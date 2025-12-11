>[!note]
>Unified Modelling Language (UML) è un linguaggio di modellazione utilizzato per lo sviluppo software, più nel dettaglio per la progettazione e l'analisi di sistemi. Rappresenta un set di notazioni e regole per creare un modello della logica interna dell'applicativo.
>
>I principali diagrammi definiti dall'UML sono i diagrammi di struttura, i diagrammi di comportamento e i diagrammi di interazione. Assieme descrivono i requisiti del sistema, quali funzionalità devono essere offerte e chi le usa, senza affrontare la descrizione di come sono realizzate.

### Class diagram
>[!note]
>Nel class diagram di hanno come nodi degli oggetti composti da quattro parti: nome, attributi, metodi e descrizione statica.
>
>Il nome è il nome della classe e la descrizione statica è la descrizione di esso. Gli attributi sono specificati con la sintassi:
>```
>visibilità nome: tipo[molteplicità] = valore predefinito
>```
>Mentre i metodi sono sono specificati con la sintassi:
>```
>visibilità nome (lista parametri): tipo di ritorno
>```
>
>Le visibilità possono essere: public `+`, private `-`, protected `#` e friendly `~`. Se un metodo non è specifico all'oggetto ma alla classe (statico) viene sottolineato.
>
>![[Pasted image 20250922143431.png|center]]
>
>Le classi possono essere associate tra loro. Un'associazione può specificare un nome e i ruoli svolti dalle classi nell'associazione. Gli estremi di un'associazione sono visti come attributi impliciti e hanno visibilità come attributi normali. Questi attributi hanno inoltre una molteplicità.
>
>![[Pasted image 20250922143648.png|center]]
>
>Per le associazioni molteplici si possono anche avere classi di associazione.
>
>![[Pasted image 20250922143749.png|center]]
>
>È possibile indicare l'ereditarietà per esplicitare eventuali comportamenti comuni.
>
>![[Pasted image 20250922150702.png|center]]
>
>Esplicitando inoltre se un elemento è una classe astratta (di cui non si possono avere esemplari) o un interfaccia.
>
>![[Pasted image 20250922150802.png|center]]


>[!tip] Aggregazioni e composizioni
>Le aggregazioni sono una forma particolare di associazione, dove una parte è in relazione con un oggetto.
>
>![[Pasted image 20250922145902.png|center]]
>
>Una relazione di composizione è un'aggregazione "forte", dove la parti componenti non esistono senza il contenitore.
>
>![[Pasted image 20250922150548.png|center]]

>[!tip] Diagramma degli oggetti
>Al contrario del diagramma delle classi il diagramma degli oggetti mostra le relazioni dirette tra le istanze delle classi.
>
>![[Pasted image 20250922150941.png|center]]

>[!tip] Package
>I package sono dei meccanismi di strutturazione, che definiscono uno spazio dei nomi. Permettono di decomporre gerarchicamente le varie classi, e inoltre permettono di specificare dipendenze tra di loro.

### Diagrammi di interazione
>[!note]
>I diagrammi di interazione descrivono il comportamento dinamico di un gruppo di oggetti che "interagiscono" per risolvere un problema. Sono utilizzati per rappresentare scenari in termini di entità e messaggi scambiati.
>
>Per farlo UML propone l'uso di diagrammi di sequenza e diagrammi di comunicazione.

>[!tip] Diagrammi di sequenza
>Il diagramma di sequenza mostra come più classi interagiscono tra loro.
>
>![[Pasted image 20250922162002.png|center]]
>
>I messaggi possono essere sincroni (freccia piena), asincroni (freccia non piena) e di risposta (freccia tratteggiata). Si può inoltre simulare delle operazioni ripetute e opzionali.
>
>![[Pasted image 20250922162117.png|center]]
>
>Si può anche simulare delle alternative.
>
>![[Pasted image 20250922162144.png|center]]

### Macchine a stati finiti
>[!note]
>Le macchine a stati finiti rappresentano il comportamento dei singoli oggetti di una classe in termini di:
>- Eventi a cui la classe è sensibile
>- Azioni prodotte
>- Transizioni di stato
>
>Di seguito la sintassi dei nodi delle macchine.
>
>![[Pasted image 20250922162426.png|center]]

>[!tip] Decomposizione OR
>Un macro stato equivale ad una scomposizione OR degli stati, dove i sottostrati ereditano le transizioni dei loro superstrati.
>
>![[Pasted image 20250922162535.png|center]]

>[!tip] Decomposizione AND
>È il caso duale al caso OR, si ha che modella operazioni ed attività concorrenti.
>
>![[Pasted image 20250922162626.png|center]]

