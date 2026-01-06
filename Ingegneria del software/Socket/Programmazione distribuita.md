>[!note]
>La programmazione distribuita in Java ha come obiettivo permettere a più programmi, in esecuzione su macchine diverse, di cooperare come se fossero parte di un unico sistema. Il problema principale non è solo la comunicazione, ma l’astrazione della rete: idealmente il programmatore dovrebbe concentrarsi sulla logica applicativa e non sui dettagli di trasmissione dei dati.

>[!tip] Modello client-server
>Il modello più classico è quello client–server, in cui un server resta in attesa di richieste e uno o più client si collegano per ottenere un servizio. In Java, il primo strumento per realizzare questo modello sono i **socket**.

### Socket
>[!note]
>Con i socket TCP, il server apre una porta e rimane in ascolto, mentre il client si collega specificando indirizzo IP e porta. Una volta stabilita la connessione, la comunicazione avviene tramite stream di input e output associati al socket.

>[!example]
>```java
>import java.net.*;
>import java.io.*;
>import java.util.*;
>
>public class EchoServer {
>    public static void main(String[] args) throws IOException {
>        ServerSocket serverSocket = new ServerSocket(4321);
>        System.out.println("Server in attesa...");
>
>        Socket socket = serverSocket.accept();
>        System.out.println("Client connesso");
>
>        Scanner in = new Scanner(socket.getInputStream());
>        PrintWriter out = new PrintWriter(socket.getOutputStream());
>
>        while (true) {
>            String line = in.nextLine();
>            if (line.equals("quit")) break;
>            out.println("Ricevuto: " + line);
>            out.flush(); // fondamentale per inviare i dati
>        }
>
>        socket.close();
>        serverSocket.close();
>    }
>}
>```
>
>```java
>import java.net.*;
>import java.io.*;
>import java.util.*;
>
>public class LineClient {
>    public static void main(String[] args) throws IOException {
>        Socket socket = new Socket("127.0.0.1", 4321);
>        System.out.println("Connessione stabilita");
>
>        Scanner socketIn = new Scanner(socket.getInputStream());
>        PrintWriter socketOut = new PrintWriter(socket.getOutputStream());
>        Scanner stdin = new Scanner(System.in);
>
>        while (true) {
>            String input = stdin.nextLine();
>            socketOut.println(input);
>            socketOut.flush();
>            System.out.println(socketIn.nextLine());
>        }
>    }
>}
>```

Questo approccio funziona, ma presenta limiti evidenti: il server gestisce un solo client alla volta e il programmatore deve occuparsi manualmente del protocollo di comunicazione. Per supportare più client, il server deve essere multi-threaded, creando un thread per ogni connessione.

>[!example]
>```java
>import java.net.*;
>import java.io.*;
>import java.util.*;
>import java.util.concurrent.*;
>
>public class MultiEchoServer {
>    public static void main(String[] args) throws IOException {
>        ServerSocket serverSocket = new ServerSocket(1337);
>        ExecutorService pool = Executors.newCachedThreadPool();
>
>        while (true) {
>            Socket socket = serverSocket.accept();
>            pool.submit(() -> {
>                try {
>                    Scanner in = new Scanner(socket.getInputStream());
>                    PrintWriter out = new PrintWriter(socket.getOutputStream());
>
>                    while (true) {
>                        String line = in.nextLine();
>                        if (line.equals("quit")) break;
>                        out.println("Ricevuto: " + line);
>                        out.flush();
>                    }
>                    socket.close();
>                } catch (IOException e) {
>                    e.printStackTrace();
>                }
>            });
>        }
>    }
>}
>```

### Java RMI
>[!note]
>Java Remote Method Invocation è un protocollo tale per cui un client può invocare metodi di un oggetto che risiede in un’altra JVM come se fosse locale. Questo è possibile grazie a oggetti remoti, interfacce remote e proxy (stub e skeleton).
>
>Il primo passo è la definizione di un interfaccia remota condivisa tra client e server che estende `Remote` e ogni metodo lancia `RemoteException`.
>
>Il server poi implementa questa interfaccia e rende l'oggetto accessibile da remoto estendendo `UnicastRemoteObject`. Questo oggetto è poi pubblicato nell'RMI Registry.
>
>Il client poi recupera lo stub dal registry e utilizza l'oggetto remoto come se fosse locale.

A runtime, RMI si occupa di serializzare i parametri, trasmetterli sulla rete, invocare il metodo sul server e restituire il risultato. Oggetti non remoti vengono passati per copia, mentre oggetti remoti vengono passati tramite riferimento allo stub.

Infine, è importante ricordare che RMI gestisce le chiamate in modo concorrente: più client possono invocare metodi simultaneamente, quindi i metodi remoti devono essere thread-safe.

Nel server:
```java
import java.rmi.*;
import java.rmi.server.*;
import java.rmi.registry.*;
import java.util.*;

public interface Warehouse extends Remote {
    double getPrice(String product) throws RemoteException;
}

public class WarehouseImpl extends UnicastRemoteObject implements Warehouse {
    private Map<String, Double> prices;

    public WarehouseImpl() throws RemoteException {
        prices = new HashMap<>();
        prices.put("Toaster", 24.95);
        prices.put("Microwave", 49.95);
    }

    public double getPrice(String product) throws RemoteException {
        return prices.getOrDefault(product, 0.0);
    }
}

public class WarehouseServer {
    public static void main(String[] args) throws Exception {
        Warehouse warehouse = new WarehouseImpl();
        Registry registry = LocateRegistry.getRegistry();
        registry.bind("central_warehouse", warehouse);
        System.out.println("Server RMI pronto");
    }
}
```

Mentre nel client:
```java
import java.rmi.*;
import java.rmi.registry.*;

public class WarehouseClient {
    public static void main(String[] args) throws Exception {
        Registry registry = LocateRegistry.getRegistry();
        Warehouse warehouse = (Warehouse) registry.lookup("central_warehouse");

        double price = warehouse.getPrice("Toaster");
        System.out.println("Prezzo: " + price);
    }
}
```