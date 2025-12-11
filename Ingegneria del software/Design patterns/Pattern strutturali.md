>[!note]
>I pattern strutturali gestiscono la composizione di oggetti e la separazione tra interfaccia e implementazione. Permettono di:
>- Utilizzare interfacce esterne.
>- Comporre oggetti a runtime.
>- Gestire l'accesso ad una moltitudine di oggetti.
>- Uniformare l'accesso ad oggetti semplici e composti.

### Adapter
>[!note]
>L'adapter pattern è usato per definire una strategia di adattamento per classi non compatibili tra loro. Per fare questo si può usare l'ereditarietà o la composizione.

```java
interface Shape {
	public Size boundingBox();
	
	// ...
}

class SquareShape implements Shape() {
	public Size boundingBox() {
		return new Size(edge * edge);
	}
	
	// ...
}

class TextView extends ExternalLibraryView {
	public Size getExtent() {
		return new Size(...);
	}
	
	// ...
}

// Usando l'ereditarietà:
class TextShape extends TextView implements Shape {
	public Size boundingBox() {
		return this.getExtent();
	}
}

// Usando la composizione
class TextShape implements Shape {
	private TextView adaptee = new TextView();
	
	public Size boundingBox() {
		return adaptee.getExtent();
	}
}
```

### Decorator
>[!note]
>Il decorator pattern definisce una classe astratta `decorator` che implementa la stessa astrazione della classe. La classe decoratrice mantiene un riferimento all'oggetto da decorare e implementazioni della classe astratta implementano decorazioni diverse.

```java
interface VisualComponent {
	void draw();
	// ...
}

class TextView implements VisualComponent {
	public void draw() {
		// ...
	}
}

abstract class Decorator implements VisualComponent {
	private VisualComponent component;
	
	public Decorator(Visualcomponent c) {
		component = c;
	}
	
	public void draw() {
		component.draw();
	}
	
	// ...
}

class BorderDecorator extends Decorator {
	public BorderDecorator(VisualComponent c) {
		super(c);
	}
	
	public void draw() {
		super.draw();
		drawBorder();
	}
	
	private void drawBorder() {
		// ...
	}
}
```