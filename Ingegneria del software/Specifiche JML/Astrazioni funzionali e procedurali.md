>[!note]
>Un'astrazione procedurale, definisce, tramite una specifica, un'operazione complessa su dati generici (o parametrici). 
 
>[!tip] Specifica
>Una specifica è una descrizione di un'entità che prescinde dall'implementazione. Nel nostro caso è un astrazione del frammento di codice, e rappresenta la classe d'equivalenza di tutte le implementazioni possibili.

In Java la signature di un metodo ne esprime la sintassi, tuttavia non ci dice nulla circa la semantica. È vantaggiosa poiché:
- L'implementazione può essere letta o scritta senza la necessità di analizzare le implementazioni di altre astrazioni.
- L'astrazione può essere re-implementata senza effetti sulle astrazioni che la usano.

È data usando un linguaggio naturale o una semplice notazione matematica.

### Java Modelling Language
>[!note]
>Java Modelling Language (JML) è un linguaggio formale di specifica basato su Java, non eseguibile dal compilatore. Le sue asserzioni possono:
>- Predicare su variabili
>- Quantificare su variabili
>- Invocare metodi puri
>- Predicare sull'invarianza di alcune variabili
>- Predicare sul corretto lancio delle eccezioni
>
>Le specifiche JML sono aggiunte al codice Java tramite commenti, che cominciano con il simbolo `@`:
>```
>//@ <JML Specification>
>
>/*@ <JML Specification> @*>
>```
>
>Funziona definendo delle precondizioni (condizioni sui parametri sotto le quali la specifica è definita e valida) e delle postcondizioni (effetti garantiti al termine dell'esecuzione dell'astrazione).

>[!tip] Programmazione per contratto
>La presenta di pre e post condizioni introduce il tema della programmazione per contratto, dove possono variare solamente le proprietà non funzionali, che non sono vincolate da esso.
>
>Le specifiche devono essere:
>- Generali: utilizzabili anche al di fuori del progetto specifico.
>- Minimali: slegate il più possibile dall'implementazione.
>- Robuste: il comportamento anomale deve essere previsto e gestito, e quindi la funzione definita deve essere totale.

I vincoli esprimibili da JML si categorizzano in:
- modifiers
- requires
- assignable
- ensures e result
- signals

>[!tip] Modifiers
>I modifiers sono delle etichette che descrivono le caratteristiche del metodo o delle variabili su cui si stanno imponendo i vincoli.
>
>`pure` si impone su metodi, e indica che il metodo non ha side effects.
>```
>//@ pure
>boolean isSorted(int[] a) { ... }
>```
>
>`model` si impone su una variabile, e permette di introdurre una variabile logica astratta che non esiste nel bytecode del programma. Questa non assume né valori né stati, e funge solo da etichetta.
>```
>//@ model int size;
>```
>
>`ghost` si impone su una variabile, e come `model` introduce una variabile non esistente nel Bytecode, tuttavia ha un valore e può cambiare durante il programma.
>```
>//@ ghost int counter;
>```
>
>Per assegnare alle variabili `ghost` si usa il modifier `set`.
>```
>//@ set counter = counter + 1;
>```

>[!tip] Requires
>`requires` impone delle precondizioni, e può essere omesso in caso una funzione sia totale.
>```
>//@ requires ...;
>```
>
>In caso la definizione di requires sia particolarmente complesso è opportuno ometterle e utilizzare `signals`.

>[!tip] Assignable
>`assignable` segnala che un'entità è mutabile, e quindi può essere modificata durante la chiamata del metodo. Si applica a parametri dei metodi, variabili, oggetti e attributi degli oggetti.
>
>```
>//@ assignable nameVar;
>```
>
>È possibile specificare che nessuna variabile che rientra nel campo di visibilità di JML viene modificata:
>```
>//@ assignable \nothing:
>```
>
>Talvolta può essere utile usare il predicato `\old`.

>[!tip] Ensures e result
>Indica le post condizioni tramite:
>```
>//@ ensures ...
>```
>
>Al suo interno si può usare il predicato `\result` che indica l'output, comparatori matematiche, formule aritmetiche complesse, metodi puri, oppure un insieme di valori indicati:
>```
>//@ ensures \result == [valore];
>
>//@ ensures Math.abs(\result * \result) < 0.1;
>```

>[!tip] Signals
>I Signals permettono di verificare post-condizioni eccezionali lanciate in caso di violazione delle requires:
>```
>//@ signals (IllegalArgumentException e) x < 0;
>```
>
>Queste si specificano indicando il tipo di eccezione e la condizione logica che indica quanto verrà lanciata.
>
>In caso esista solo un tipo di eccezione lanciabile dal metodo si può usare:
>```
>//@ signals_only (IllegalArgumentException e) x < 0;
>```

È necessario che le condizioni delle Signals e Ensures siano ortogonali tra loro.

>[!tip] Altre clasusole e commenti
>Esistono dei predicati in JML, oltre a quelli visti, che non rientrano in alcuna categoria, questi sono:
>- `a ==> b`: `a` implica `b`.
>- `a <== b`: `b` implica `a`.
>- `a <==> b`: `a` se e solo se `b`.
>- `a <=!=> b`: not `a` se e solo se `b`.
>- `\old(E)`: valore di `E` precedente all'esecuzione del codice.
>- `(* ... *)`: commenti testuali, da usare se i vincoli sono estremamente difficili da esprimere.

>[!tip] Quantificatori
>JML supporta diversi tipi di quantificatori, tra cui:
>- Universale (`\forall`) ed Esistenziale (`\exists`).
>- Funzioni quantificatrici (`\sum`, `\product`, `\min`, `\max`).
>- Quantificatore numerico (`\num_of`).
>
>In JML questi hanno una forma a tre campi:
>```
>(\forall Tipo v; range; condizione)
>```
>Dove il primo campo indica il tipo e il nome della variabile su cui predichiamo, il secondo campo indica il dominio ristretto in cui JML deve operare, e l'ultimo campo è il predicato che deve essere soddisfatto da ogni elemento del range.
>
>Nelle funzioni quantificatrici e quantificatore numerico l'ultimo campo agisce come filtro che determina quali valori contare.

