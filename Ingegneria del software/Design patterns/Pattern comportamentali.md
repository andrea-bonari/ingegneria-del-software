>[!note]
>I pattern comportamentali definiscono il comportamento e le modalità di interazione tra oggetti. Permettono di:
>- Gestire la dipendenza nelle funzionalità tra classi e sottoclassi.
>- Tenere traccia delle azioni compiute da un oggetto.
>- Definire comportamenti diversi per oggetti definiti in una gerarchia.
>- Modificare il comportamento di un oggetto a runtime.

### Command
>[!note]
>Il command pattern definisce un'interfaccia `Command`, la cui struttura più semplice è che contenga un solo metodo `execute`. Ogni oggetto che esegue il comando ha un riferimento ad un oggetto di tipo `Command`, in questo modo l'azione da compiere diventa slegata dagli oggetti che la usano.

```java
interface Command {
	void execute();
	// ...
}

class PasteCommand implements Command {
	private Document doc;
	
	public PasteCommand(Document doc) {
		this.doc = doc;
	}
	
	public void execute() {
		// ...
	}
}

class Menu {
	List<MenuItem> items = new ArrayList<>();
	
	public void addMenuItem(MenuItem a) {
		// ...
	}
}

class MenuItem {
	Command command;
	
	public void setCommand(Command cmd) {
		this.command = cmd;
	}
	
	public void onClick() {
		command.execute();
	}
}
```

### Observer
>[!note]
>L'observer pattern definisce un sistema astratto per la comunicazione one-to-many. Per farlo crea una classe astratta `Observable`, per rappresentare la sorgente di dati, che contiene una lista di `Observer`, che rappresentano gli utilizzatori dei dati. Gli oggetti `Observer` possono iscriversi/disiscriversi agli aggiornamenti di `Observable` attraverso appositi metodi.

```java
abstract class DataSource {
	List<DataListener> listeners = new ArrayList<>();
	
	public addListener(DataListener ld) {
		listeners.add(ld);
	}
	
	public removeListener(DataListener ld) {
		listeners.remove(ld);
	}
	
	protected updateAll(float data[][]) {
		for(DataListener ld : listeners) {
			ld.update(data);
		}
	}
}

class Spreadsheet extends DataSource {
	private float data[][];
	
	// ...
	
	private void updateData(int x, int y, float value) {
		data[x][y] = value;
		this.updateAll(data);
	}
}

interface DataListener {
	update(float data[][]);
}

class BarChart implements DataListener {
	public void update(float data[][]) {
		// ...
		draw();
	}
	
	private void draw() {
		// ...
	}
}
```

### Strategy
>[!note]
>Lo strategy pattern definisce un'interfaccia `Strategy`, in cui ogni implementazione implementa un diverso algoritmo. Poi un elemento `Composition` avrà un riferimento ad una `Strategy` (non modificabile a runtime).

```java
interface Compositor {
	void compose(Data data);
}

class SimpleCompositor implements Compositor {
	public void compose(Data data) {
		// ...
	}
}

class Composition {
	private Data data;
	private Compositor compositor;
	
	public void setCompositor(Compositor cmp) {
		compositor = cmp;
	}
	
	public void traverse() {
		// ...
	}
	
	public void repair() {
		compositor.compose(data);
	}
}
```

### State
>[!note]
>Lo state pattern è usato per rappresentare un FSA (Automa a Stati Finiti). Per farlo si definisce una classe `State`, dove ogni sua sottoclasse gestisce le operazioni relative allo stato ed effettua la transizione al prossimo stato. Lo stato attuale è referenziato dall'oggetto che sta usando l'FSA. Questo approccio suddivide la logica applicativa in più classi, rendendolo più mantenibile.

```java
abstract class TCPState {
	protected TCPConnection connection;
	
	public TCPState(TCPConnection connection) {
		this.connection = connection;
	}
	
	abstract public void open();
	abstract public void close();
	abstract public void acknowledge();
	
	public void transition(TCPState state) {
		connection.setState(state);
	}
}

public class TCPListen extends TCPState {
	public TCPListen(TCPConnection connection) {
		super(connection);	
	}
	
	public void open() {
		// ...
		this.transition(new TCPEstabilished(connection));
	}
	
	public void close() {
		// ...
	}
	
	public void acknowledge() {
		// ...
	}
}

class TCPConnection {
	private TCPState state;
	
	public TCPConnection() {
		state = new TCPListen(this);
	}
	
	public void setState(TCPState newState) {
		state = newState;
	}
	
	public void open() {
		state.open();
	}
	
	public void close() {
		state.close();
	}
	
	public void acknowledge() {
		state.acknowledge();
	}
}
```