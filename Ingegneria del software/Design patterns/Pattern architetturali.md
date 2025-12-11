>[!note]
>I pattern architetturali definiscono metodologie per la creazione di applicazioni e sistemi software. Sono spesso alla base di framework. Permettono di:
>- Separare modello e "view".
>- Gestire la comunicazione tra i diversi livelli logici di un sistema.

### Model-View-Controller
>[!note]
>Il pattern Model-View-Controller (MVC) suddivide lo sviluppo in tre componenti:
>- `Model`: contiene lo stato e la logica applicativa e non ha dipendenze con altri componenti.
>- `View`: contiene la logica di visualizzazione del `Model`, può avere un riferimento al `Model`.
>- `Controller`: riceve gli input degli utenti inoltrati dalla `View`, modifica poi `Model` e `View`.
>
>Ne esistono diverse variazioni.
>
>Di seguito un grafico rappresentante la sua struttura:
>![[Pasted image 20251124173824.png|center]]

```java
class Calculator extends CalculatorObservable {
	float result = 0;
	String expression = "";
	
	private void compute() {
		// ...
		notifyAll();
	}
	
	private float power() {
		// ...
	}
	
	private float factorial() {
		// ...
	}
	
	public float getResult() {
		return result;
	}
}

class CalculatorController implements onClickListener {
	ComputeButton button;
	Calculator calculator = new Calculator();
	
	public void setComputeButton(ComputeButton button) {
		this.button = button;
		this.button.addOnClickListener(this);
	}
	
	public void onClick() {
		calculator.compute();
	}
	
	// ...
}

class ComputeButton extends Button {
	// Riceve input utente
}

class ResultTextField extends TextField implements CalculatorListener {
	Calculator calc;
	
	public ResultTextField(Calculator c) {
		calc = c;
		c.addObserver(this);
	}
	
	public void updateResult() {
		setText(String.valueof(calc.getResult()));
	}
}
```

>[!tip] Model-View-Presenter
>Model-View-Presenter (MVP) è come la MVC, tuttavia non ha dipendenze sul modello. La comunicazione Controller-View avviene con interfacce:
>- `Model`: contiene lo stato e la logica applicativa e non ha dipendenze con altri componenti.
>- `View`: contiene la logica di visualizzazione, propaga gli eventi al `Presenter`.
>- `Presenter`: riceve gli input degli utenti inoltrati dalla `View`, modifica il modello e la `View`.
>
>![[Pasted image 20251124174858.png|center]]

>[!tip] Model-View-ViewModel
>Model-View-ViewModel (MVVM), come MVP, riduce ulteriormente le dipendenze tra livelli.
>- `Model`: contiene lo stato e la logica applicativa e non ha dipendenze con altri componenti.
>- `View`: non contiene logica, di solito è create con linguaggi dichiarativi.
>- `ViewModel`: non ha riferimenti alla `View` né ad interfacce relative. Prepara un insieme di dati (solitamente primitivi) pensati per la visualizzazione (observable), esponendo metodi per reagire agli input degli utenti.
>
>Contiene anche dei data binding, cioè un insieme di componenti dedicati a collegare `View` e `ViewModel` (solitamente forniti da un framework). L'utente nella definizione della view può sottoscriversi ad un specifico `ViewModel` e ai relativi dati.
>
>![[Pasted image 20251124175228.png|center]]

