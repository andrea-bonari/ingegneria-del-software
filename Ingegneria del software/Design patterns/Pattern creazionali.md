>[!note]
>I pattern creazionali definiscono metodologie per la creazione di oggetti. Permettono di:
>- Gestire la dipendenza tra creatore e creato a compile time.
>- Limitare il numero di istanze di una classe.
>- Utilizzare la clonazione.
>- Gestire la creazione di tipi complessi e fortemente parametrici.

### Factory method
>[!note]
>Il factory method pattern consiste nella definizione della classe astratta, con un metodo astratto `factory` per la creazione di oggetti, di cui le sottoclassi conosceranno il tipo da istanziare. Il pattern delega la creazione di oggetti alle sottoclassi, permettendo alla superclasse di non contenere dipendenze con tipi specifici.

```java
class Product { ... }
class ConcreteProduct extends Product { ... }

abstract class Creator {
	abstract public Product FactoryMethod();
	
	// Qualsiasi altra operazione
}

class ConcreteCreator extends Creator {
	public Product FactoryMethod() {
		return new ConcreteProduct();
	}
}
```

### Abstract Factory
>[!note]
>L'abstract factory pattern consiste nella definizione di classi `factory` dedicate a generare elementi appartenenti ad una gerarchia. Un'interfaccia o una classe astratta definiscono le funzionalità delle factory. I client non creano quindi direttamente gli oggetti ma utilizzano una factory. In questo modo modificare la tipologia di elementi da creare equivale a cambiare istanza di factory.

```java
abstract class WidgetFactory {
	public abstract Window createWindow();
	public abstract Panel createPanel();
	public abstract Button createButton();
	public abstract Scrollbar createScrollbar();
	
	// ...
}

class PMWidgetFactory extends WidgetFactory {
	public Window createWindow(){
		return new PMWindow();
	}
	
	public Panel createPanel(){
		return new PMPanel();
	}
	
	public Button createButton(){
		return new PMButton();
	}
	
	public Scrollbar createScrollbar(){
		return new PMScrollbar();
	}
	
	// ...
}

class MotifWidgetFactory extends WidgetFactory {
	public Window createWindow(){
		return new MotifWindow();
	}
	
	public Panel createPanel(){
		return new MotifPanel();
	}
	
	public Button createButton(){
		return new MotifButton();
	}
	
	public Scrollbar createScrollbar(){
		return new MotifScrollbar();
	}
	
	// ...
}
```

