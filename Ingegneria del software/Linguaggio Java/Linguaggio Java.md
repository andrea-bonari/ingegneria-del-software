>[!note]
>Java è un linguaggio di programmazione orientato agli oggetti. Ai tempi fu molti innovativo, poiché era un linguaggio di programmazione che poteva essere eseguito su più piattaforme.
>
>Il linguaggio è fortemente e staticamente tipizzato.

Java ha un passaggio di compilazione, che trasforma il codice in un linguaggio intermedio, detto bytecode. Il codice bytecode viene poi interpretato dalla Java Virtual Machine (JVM), permettendo quindi a Java di essere eseguito da più piattaforme, a patto che abbiano installato la JVM.

Di seguito un semplice programma in Java:
```java
public class Prova {
	public static void main(String args[]) {
		System.out.println("Hello World");
	}
}
```

### Modificatori di accesso
>[!note]
>I modificatori di accesso stabiliscono delle restrizioni sull'accesso ad attributi e metodi di una classe da parte di altre classi. In Java sono presenti tre tipologie di modificatori:
>- `public`: non pone alcuna restrizione sull'accesso ad un determinato membro.
>- `private`: indica che è possibile accedere al membro solamente all'interno della classe in cui è definito.
>- `protected`: indica che è possibile accedere al membro solamente all'interno dello stesso package in cui è contenuta la sua classe, e alle sue sottoclassi.

Per rispettare i paradigmi della programmazione ad oggetti gli attributi di una classe devono essere `private`, mentre devono esistere dei metodi getter e setter `public`.

### Costruzione e allocazione di classi
>[!note]
>Per creare allocare una classe si usa l'istruzione `new Classe()`, che ha l'effetto di chiamare un costruttore, cioè un metodo speciale che ha come compito l'allocazione della memoria e l'inizializzazione degli attributi.
>
>Di base esiste il costruttore di default che non accetta parametri in ingresso ed inizializza ogni attributo dell'oggetto con un valore di default, tuttavia è possibile scrivere costruttori propri, con la sintassi:
>```java
>public class Data {
>	// Attributi vari
>	
>	public Data(int giorno, int mese, int anno) {
>		this.giorno = giorno;
>		this.mese = mese;
>		this.anno = anno;
>	}
>}
>```
>
>Il costruttore può essere poi richiamato eseguendo:
>```java
>public class Main {
>	public static void main(String args[]) {
>		Data d = new Data(30, 9, 2025);
>	}
>}
>```
>
>Si può eseguire anche l'overloading sui costruttori.

>[!tip] Overloading
>L'overloading consiste nell'avere più funzioni con lo stesso nome ma con liste di parametri diverse. In questo modo il compilatore è in grado di distinguere quale versione utilizzare in base agli argomenti passati.
>
>Nel caso dei costruttori si stabilisce un costruttore "principale" e gli altri secondari. È possibile richiamare il costruttore principale utilizzando la parola chiave `this()` per evitare di duplicare il codice.

>[!tip] Allocazione e GC
>Quando usiamo il tipo `Classe` viene creato un riferimento nello stack del metodo in esecuzione, che può puntare ad un oggetto in memoria nell'heap. Quando poi creeremo la classe con un costruttore questa sarà allocata nell'heap, e l'istruzione `new` restituisce un riferimento, assegnabile al riferimento nello stack.
>
>In Java inoltre, la gestione della memoria è automatica. Quando una parte di memoria non è più esplicitamente richiesta il Garbage Collector (GC), che si attiva periodicamente, individua e rimuove gli oggetti non più raggiungibili da alcun riferimento diretto o indiretto.
>Questo introduce un leggero costo in termini di prestazioni, poiché deve analizzare lo stato degli oggetti in memoria, tuttavia il vantaggio è enorme.

### Ereditarietà e polimorfismo
>[!note]
>L'ereditarietà consente di stabilire una relazione "sottoclasse di" fra delle classi. In Java l'ereditarietà è singola e si definisce tramite la parola chiave `extends`. 
>La sottoclasse eredita tutta l'implementazione, cioè attributi e metodi della superclasse.
>
>In caso la superclasse abbia dichiarato un costruttore esplicitamente è necessario scrivere un costruttore che chiami quello esplicito tramite la parola chiave `super()`.
>
>Infine una sottoclasse può ridefinire un metodo ereditato tramite il decorator `@override`.

Si ha che l'assegnamento:
```java
Superclasse p = new Sottoclasse(...);
```
È valido, tuttavia non è valido:
```java
Sottoclasse p = new Superclasse(...);
```

### Specifica static
>[!note]
>La specifica `static` rende l'elemento a cui è assegnata appartenente all'intera classe, anziché ad una sua singola istanza, di fatto rendendolo un singolo elemento unico e condiviso.
>
>```java
>public class Utils {
>	public static void swap(int[] v1, int[] v2) {
>		int[] temp = { v1[0] };
>		v1[0] = v2[0];
>		v2[0] = temp[0];
>	}
>}
>
>public class Main {
>	public static void main(String[] args) {
>		int[] thirtythree = { 33 };
>		int[] nine = { 9 };
>		Utils.swap(thirtythree, nine);
>		System.out.println(thirtythree[0] + " and " + nine[0]);
>	}
>}
>```

### Specifica final
>[!note]
>La specifica `final` indica che le variabili dichiarate con essa possono essere assegnate solo una volta. Se la variabile `final` contiene una reference all'oggetto allora l'oggetto è comunque mutabile, ma la variabile si riferisce sempre allo stesso oggetto.
>
>È lecito usare `final` anche su variabili locali e parametri.
>
>Quando si marca un metodo con `final` questo non può essere sovrascritto o nascosto. 

Nelle classi si può marcare gli attributi come `final` e poi inizializzarle nel costruttore.
### Switch
>[!note]
>In java l'istruzione `switch` può essere sia uno statement che un espressione, e quindi può restituire un valore come può non farlo. La sintassi dello statement è:
>```java
>switch(obj)
>	case 0 -> System.out.prinln("test");
>	case 1 -> {
>		// Multiline code block
>	}
>	default -> System.out.prinln("tutti gli altri valori");
>```
>Mentre la sintassi della expression è:
>```java
>String result = switch(obj) {
>	case 1 -> "valore final costante"
>	case 2 -> {
>		// multiriga terminato da
>		yield "valore multiriga"
>	}
>	default -> "default obbligatorio"
>}
>```

### Enum
>[!note]
>Gli `enum` sono delle vere e proprie classi le cui istanze sono predefinite, per esempio:
>```java
>public enum CourseType {
>	ENG("Engineering"),
>	ARCH("Architechture"),
>	DES("Design"),
>	INVALID("Invalid");
>	
>	private String name;
>	
>	public CourseType(String name) {
>		this.name = name;
>	}
>}
>```

### Specifica abstract
>[!note]
>La specifica `abstract` indica che le classi, metodi e attributi così specificati non sono completamente definiti ed hanno bisogno di sottoclassi non astratte per poter essere istanziate. Di conseguenza le classi astratte non esistono autonomamente, e sono solo modelli per le sottoclassi. Per esempio
>
>```java
>public abstract class Polygon {
>	private final int edges;
>	
>	public Polygon(int edges) {
>		this.edges = edges;
>	}
>	
>	public int getEdges() {
>		return edges;
>	}
>	
>	public abstract void draw();
>}
>
>public class Triangle extends Polygon {
>	public Triangle() {
>		super(3);
>	}
>	
>	@override
>	public void draw() {
>		System.out.prinln("▲");
>	}
>}
>```

### Interfacce
>[!note]
>Un interfaccia è una classe che impone l'implementazione delle funzionalità scelte nella classe a cui è assegnata. Per definizione l'interfaccia ha solamente metodi astratti, pertanto la specifica è implicita.
>
>Per ogni classe a cui la si vuole imporre basterà aggiungere `implements` nella dichiarazione della classe.
>
>Per esempio:
>
>```java
>public interface Drawable {
>	public void draw();
>}
>
>public abstract class Polygon implements Drawable {
>	// ...
>}
>```

