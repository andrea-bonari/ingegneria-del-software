>[!note]
>La programmazione ad oggetti è un paradigma progettuale di programmazione informatica che descrive la struttura dati (oggetto) e le operazioni eseguibili su queste stesse strutture.
>
>In generale questo approccio favorisce il riuso di codice, la modularizzazione e permette l'incapsulamento dei dati.

>[!tip] Riuso
>Il riuso di codice permette di ridurre i tempi di sviluppo e manutenzione, aumenta la robustezza ed affidabilità, e migliora l'efficienza. Per utilizzare il riuso tuttavia i moduli devono essere facilmente adattabili.

>[!tip] Modularizzazione
>Un sistema è detto modulare se è diviso in parti che hanno una sostanziale autonomia individuale ed una ridotta interazione con le altre parti. Quindi i moduli sono scarsamente connessi e fortemente coesi.
>
>In generale con il termine modulo intendiamo un fornitore di risorse computazionali come procedure, strutture dati e tipi. È importante distinguerne l'interfaccia, cioè come il modulo entra in contatto con i suoi utilizzatori, e l'implementazione.
>
>Una buona modularizzazione costituisce la precondizione al riuso del codice, e influenza positivamente le altre qualità interne al software.
>
>Tradizionalmente si utilizza una decomposizione "top-down", dove si scompone ricorsivamente la funzionalità principale del sistema da sviluppare in funzionalità più semplici, tuttavia questo approccio non risulta adatto a progettare sistemi di grosse dimensioni. In questi casi si utilizza il concetto di astrazione.

>[!tip] Incapsulazione
>L'incapsulazione dei dati è un concetto per cui ogni modifica alla struttura dati resta confinata alla struttura stessa. Questo concetto prevede l'accesso e la modifica di un informazione non diretta, ma tramite un interfaccia. Questo permette di modificare l'implementazione senza dover eseguire cambiamenti in tutto il codice.

Un tipo di dato astratto (ADT) è un astrazione sui dati che non classifica i dati in base alla loro rappresentazione (implementazione), ma in base al loro comportamento atteso (interfaccia).

Le operazioni all'interfaccia sono le sole che si possono utilizzare per creare, modificare ed accedere agli oggetti, in questo modulo si applica l'incapsulazione dei dati.

Il linguaggio C non ha costrutti specifici per l'ADT, tuttavia utilizzando il preprocessore, gli header file, puntatori e prototipi si può separare interfaccia e implementazione, pertanto esistono un certo numero di linguaggi di programmazione orientati agli oggetti.

Questi linguaggi obbligano ad incapsulare le strutture dati all'interno di opportune dichiarazioni (classi), consentono di impedire facilmente l'accesso all'implementazione e rendono possibile creare istanze concrete da un'astrazione per parametrizzazione. In questi linguaggi costruttori e metodi sono procedure che appartengono agli oggetti ed operano in maniera implicita sull'oggetto a cui appartengono.

### Orientamento agli oggetti
>[!note]
>Definiamo un oggetto come un concetto, un'astrazione o, in generale, un'entità avente un significato ben preciso per l'applicazione in esame. Esso è composto da un identità, un comportamento ed uno stato.
>
>Lo stato rappresenta la condizione in cui si trova l'oggetto, ed è definito dai valori delle proprietà (attributi). Questi possono essere mutabili o immutabili. Un oggetto può essere a sua volta composto da altri oggetti.
>
>Il comportamento determina come agisce e reagisce uno stato, e quindi i suoi cambiamenti di stato e razioni ad azioni di altri oggetti. È definito dall'insieme di operazioni che l'oggetto può compiere.
>
>L'identità degli oggetti è univoca, ed è definita dalla locazione di memoria nei linguaggi di programmazione tradizionali. Pertanto due oggetti possono essere uguali (stesso valore dello stato) oppure identici (stesso oggetto).

>[!tip] Classi
>Una classe è un gruppo di entità identificato da un insieme di caratteristiche comuni, è quindi un modello per creare oggetti con proprietà simili. La classe è un astrazione della realtà. È necessario che ogni classe catturi una ed una sola astrazione.
>
>Le proprietà di una classe si dividono in pubbliche e private. Quelle private sono visibili e modificabili solamente attraverso apposite proprietà pubbliche.
>
>Un oggetto è un istanza di una classe, e pertanto una classe descrive un insieme di oggetti aventi la stessa struttura.
>

I diversi oggetti che costituiscono un'applicazione comunicano attraverso lo scambio di messaggi, e quindi a seguito della ricezione di un messaggio viene invocato un metodo dell'oggetto ricevente.

Esistono quindi diverse relazioni fra classi, tra cui ereditarietà, aggregazione e uso.

### Ereditarietà
>[!note]
>L'ereditarietà definisce una relazione fra classi. In generale una classe (sottoclasse) condivide (eredita) la struttura e/o il comportamento di altre classi (sopraclassi).
>
>In generale le proprietà sono definite al livello più alto possibile della gerarchia, poiché le sottoclassi ereditano tutte le proprietà. Le sottoclassi possono poi aggiungere proprietà o modificare quelle esistenti.
>
>Una classe può ereditare da più classi, in questo caso si parla di ereditarietà multipla. In caso di ereditarietà multipla la gerarchia di ereditarietà diventa un grafo. L'ereditarietà multipla comporta ambiguità dei nomi causata dagli stessi nomi usati in più sopraclassi, tuttavia la soluzione a questo problema dipende dal linguaggio. Inoltre l'ereditarietà multipla comporta una scarsa efficienza nella ricerca dei metodi, tuttavia anche questo problema si risolve usando meccanismi di caching.

L'ereditarietà permette di generalizzare e specializzare. Per il processo di generalizzazione si creano delle sopraclassi che fattorizzano le proprietà comuni a diverse classi, mentre per la specializzazione si creano sottoclassi che definiscono i raffinamenti della sopraclasse.

### Polimorfismo
>[!note]
>Definiamo il polimorfismo come la capacità di un'entità di assumere forme diverse nel corso della propria esistenza. Tanto è vero che una variabile poliformica può "mutare" il proprio tipo, si crea infatti il distinguo tra tipo statico della variabile e il tipo dinamico.
>
>Il polimorfismo è comunque possibile anche in linguaggi con tipizzazione statica in presenza di ereditarietà. Essa consente di assegnare ad una variabile il cui tipo sia una classe $A$, il riferimento ad oggetti che siano istanze di una qualsiasi sottoclasse di $A$.

>[!tip] Late Binding
>Si nota che i metodi possono essere modificati dalle classi che li ereditano, e quindi ci possono essere più metodi con lo stesso nome e funzionalità diverse. In questo caso il legame fra il nome di una funzione ed il codice da eseguire non avviene in fase di compilazione (static binding), ma avviene in fase di esecuzione, all'atto della chiamata (late bindind).

