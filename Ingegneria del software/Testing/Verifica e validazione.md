>[!note]
>È importante verificare e validare un sistema software affinché soddisfi i bisogni dell'utente. "Verificare" significa controllare la corrispondenza del software alla sua specifica, mentre "Validare" significa controllare se il software fa ciò che l'utente ha realmente chiesto.

Ogni fase del processo di sviluppo dovrebbe essere verificata, per scoprire difetti il prima possibile, e accertarsi dell'usabilità del sistema nel dominio applicativo.

### Verifiche dinamiche
>[!note]
>Generalmente durante il processo di testing si sollecita e si osserva il comportamento del prodotto. Questo può avvenire staticamente (attraverso ispezioni manuali o esecuzione di strumenti automatici di analisi) o dinamicamente.

I test dei programmi coprono una frazione dell'insieme dei casi possibili.

### Analisi statica automatica
>[!note]
>L'analisi statica è una tecnica che consente di analizzare dei semielaborati software senza eseguirli, è eseguita da strumenti automatici, al contrario delle ispezioni, che sono condotte da persone.
>
>Gli strumenti di analisi possono seguire due approcci:
>- Rigoroso: si segnalano solo certi errori, tralasciando quelli possibili. L'utente deve sapere se l'analisi si conclude senza errori, questo non significa che non ce ne siano.
>- Pessimistico: si segnalano sia gli errori certi che quelli possibili. Se non si segnalano errori vuol dire che non ce ne sono. L'utente deve sapere che a fronte di una segnalazione deve verificare se si tratta di un difetto reale o no.

Generalmente le analisi statiche forniscono dati su:
- variabili definite ma non usate (difficile stabilire in linguaggi con puntatori, si usano gli alias).
- Accesso ad array fuori dai limiti.
- Codice irraggiungibile.
- Sottoprogrammi dichiarati ma non usati.

L'analisi si concentra su problemi riguardo al flusso di controllo, uso dei dati o interfacce.

Ci sono molte limitazioni dovute alla non decidibilità di molte caratteristiche interessanti.