>[!note]
>La JVM permette di gestire l'esecuzione simultanea di più thread o task. Di base il modello di multitasking è preemptive:
>- Il SO ha totale controllo sull'assegnazione del tempo di esecuzione ai vari processi o thread.
>- Ogni thread non può direttamente accedere alla CPU ma la sua esecuzione è interrotta dopo che scade il quanto di tempo che gli viene assegnato dallo scheduler.
>- Le risorse sono equidistribuite su ogni thread in esecuzione.
### Thread
>[!note]
>Un thread è un'unità di esecuzione indipendente all'interno di un programma che permette di gestire in parallelo più flussi di esecuzione. Queste unità sono implementate tramite la classe `Thread` che implementa `runnable`, nel quale è contenuto il metodo `run()` che contiene il codice eseguito dal thread. Solitamente si usa la sintassi mutata dalla programmazione funzionale:
>```java
>public class ThreadMain {
>	public static void main(String[] args) {
>		for(int i = 0; i < 1000; i++) {
>			new Thread(() -> System.out.println("Hello")).start();
>		}
>	}
>}
>```
>Tuttavia è possibile definirlo con la sintassi:
>```java
>public class MyThread extends Thread {
>	public void run() {
>		System.out.println("Hello");
>	}
>}
>
>public class ThreadMain {
>	public static void main(String[] args) {
>		Thread t = new MyThread();
>		t.start();
>	}
>}
>```

I metodi della classe Thread sono:
- `start()`: avvia l'esecuzione di un thread impostandone lo stato RUNNABLE.
- `run()`: contiene il codice eseguito dal thread.
- `sleep(long millis)`: sospende l'esecuzione del thread per `millis` millisecondi.
- `join()`: il thread chiamante aspetta la fine del thread su cui è invocato.
- `interrupt()`: viene impostato un flag di interruzione, non fermandone l'esecuzione istantaneamente.
- `isInterrupted()`: ritorna `true` se il thread è stato interrotto, `false` altrimenti.
- `interrupted()`: controlla se il thread è stato interrotto e nel caso ne resetta il flag di interruzione.

>[!tip] Istruzione `synchronized`
>Il metodo `synchronized(obj)` è utilizzato per evitare situazioni di race condition, permettendo che che certi metodi siano eseguiti in mutua esclusione, cioè che i codici non possano accedere alla stessa risorsa contemporaneamente.
>
>Il metodo `synchronized(obj)` usa l'oggetto `obj` come lock: mentre è attivo il lock su un certo oggetto nessun'altro codice che sia sincronizzato sullo stesso oggetto può essere eseguito.
>
>```java
>public class BankAccount {
>	private int balance;
>	
>	public void deposit(int amount) {
>		synchronized(this) {
>			balance = balance + amount;
>		}
>	}
>	
>	public synchronized void withdraw(int amount) {
>		balance = balance - amout;
>	}
>	
>	public int getBalance() {
>		synchronized(this) {
>			return balance;
>		}
>	}
>}
>```
>
>Il calcolo del lock viene fatto rispetto all'istanza dell'oggetto a cui è legato.
>
>È necessario porre molta attenzione poiché l'uso di `synchronized` potrebbe causare problemi di liveliness del programma, cioè si potrebbero verificare deadlock (reciprocità di due thread infinita), starvation (difficoltà di un thread ad accedere ad una risorsa condivisa) e livelock (errore che genera una sequenza ciclica di operazioni inutili).
>
>I costruttori non possono essere `synchronized`.
>
>Per gestire l'esecuzione concorrente di più thread `Object` implementa dei metodi che possono essere usati solo all'interno del blocco `synchronized` (altrimenti causano un eccezione):
>- `wait()`: sospende l'esecuzione del thread mettendolo in attesa, finché non è risvegliato da una `notify()` o una `notifyAll()`. Subito dopo la messa in stato di attesa il lock sull'oggetto è rilasciato.
>- `wait(long timeout)`: sospende l'esecuzione del thread per un determinato lasso di tempo di `timeout` millisecondi.
>- `notify()`: risveglia un solo thread in attesa sull'oggetto. Riprendendosi il lock sull'oggetto.
>- `notifyAll()`: esegue `notify()` su tutti i thread in attesa.

>[!tip] `ReadWriteBlock`
>Quando i dati vengono letti frequentemente ma modificati raramente sincronizzare completamente ad ogni accesso è inefficiente, si usa quindi l'interfaccia `ReadWriteLock`, implementata da `ReentrantReadWriteLock`. Questa classe fornisce due tipi di lock:
>- `readLock()`: condiviso
>- `writeLock()`: esclusivo
>
>Questo meccanismo permette letture parallele garantendo che solo un thread per volta possa scrivere.
>
>```java
>public class AddressBook {
>	private final ReadWriteLock lock = new ReentrantReadWriteLock();
>	private final Map<String, Integer> numbers = new ConcurrentHashMap<>();
>	
>	public void add(String name, Integer number) {
>		lock.writeLock().lock();
>		try {
>			numbers.put(name, number);
>		} finally {
>			lock.writeLock.unlock();
>		}
>	}
>	
>	public int getNumber(String name) {
>		lock.readLock().lock();
>		try {
>			return numbers.get(name);
>		} finally {
>			lock.readLock().unlock();
>		}
>	}
>}
>
>```

### Thread Pool
>[!note]
>Il thread pool è un meccanismo applicato per evitare la continua creazione e distribuzione di thread per l'esecuzione di un solo task. Sono dei thread pre-creati e riutilizzabili che vengono gestiti da un framework per eseguire più attività in modo efficiente, senza dover creare e distruggere thread ogni volta. Java fornisce di base la classe `ExecutorService`
>
>```java
>ExecutorService executor = Executors.newFixedThreadPool(NUMERO_THREAD);
>
>executor.submit(() -> System.out.println("Hello!"));
>```
>
>Il tipo di funzione può essere `Runnable` (per i metodi che non restituiscono risultato) o `Callable` (per i metodi che producono risultato).
>
>Dopo aver finito di eseguire i task è normale chiudere la pool thread, grazie al metodo `.shutdown()` e le sue varianti.

### Futures
>[!note]
>`Future` è un'interfaccia che "promette" il risultato futuro di un'operazione eseguita in un thread separato. Quando si lancia un thread asincrono il metodo che lo avvia restituisce un `Future` che è possibile utilizzare per recuperare il risultato una volta terminato.
>
>Per avviare un `Future` si usa un `ExecutorService`. Il problema principale di questa interfaccia è che i metodi non sono componibili, e per interagire con un `Future` esistono i metodi:
>- `get()`: blocca finché non finisce e viene restituito il risultato.
>- `isDone()`: controlla se è finito.
>- `cancel()`: prova ad annullarlo.

>[!tip] Classe `CompletableFuture`
>Questa classe rappresenta il completamente asincrono di un'operazione, supportando anche più operazioni asincrone, callback e completamento manuale. I metodi disponibili sono:
>- `thenApply(Function<T,R> fn)`: trasforma il risultato e ritorna un nuovo `CompletableFuture`.
>- `thenApplyAsync(Function <T,R> fn)`: trasforma il risultato in un altro thread, che restituisce un altro `CompletableFuture()`. Se non metto l'esecutore ne è scelto uno di default.
>- `supplyAsync(Supplier<T> s, Executor ex)`: avvia un task asincrono che produce un risultato.
>- `thenAccept(Consumer<T> consumer)`: consuma il risultato, ritorna void.
>- `thenAcceptAsync(Consumer<T> consumer)`: consume il risultato in un altro thread.
>- `get()`: blocca finché non finisce l'esecuzione e viene restituito il risultato.

### Variabili atomiche
>[!note]
>Per rendere un l'accesso a un tipo base thread safe possiamo utilizzare le classe atomiche relative fornite da Java, che permettono di lavorare su una variabile in modo interamente thread-safe senza usare `synchronize()`.
>
>```java
>public class BankAccountAtomic {
>	private AtomicInteger balance;
>	
>	public BankAccountAtomic() {
>		this.balance = new AtomicInteger();
>	}
>	
>	public void withdraw(int amount) {
>		balance.addAndGet(-amount);
>	}
>	
>	public void deposit(int amount) {
>		balance.addAndGet(amount);
>	}
>	
>	public int getBalance() {
>		return balance.get();
>	}
>}
>```

### Collections Concorrenti
>[!note]
>Di base tutte le collections in Java non sono nativamente thread safe, tuttavia per alcune collection ne esistono versioni sincronizzate. Per esempio:
>- `ConcurrentHashMap`: permette accessi paralleli senza dover sincronizzare manualmente tutto il blocco, usando lock striping così che i thread possano operare su parti diverse della mappa contemporaneamente.
>- `CopyOnWriteArrayList`: le operazioni di scrittura creano una nuova copia dell'intero array interno, mentre le letture avvengono su snapshot immutabili e non richiedono lock, eliminando race conditions ma rendendo le scritture molto costose.
>- `CopyOnWriteArraySet`: come per il `CopyOnWriteArrayList`.


