>[!note]
>Il black-box testing è il collaudo di un oggetto ignorando la sua organizzazione e il suo funzionamento interno. Per farlo consideriamo il programma come una scatola nera e creiamo i casi di test a partire da un'analisi delle specifiche dei requisiti.
>
>Questo permette al test di essere pianificato presto, perché dipende solo dalle specifiche.

Questa tecnica richiede specifiche precise e poca ambiguità.

>[!tip] Testing guidato dalla sintassi
>Questo criterio è utile per programmi che interpretano testi secondo una grammatica formale. L'idea è che le stesse regole che il programma da testare deve osservare/riconoscere vengono usate per generare dati di ingresso per quel programma.
>
>La grammatica fa parte delle specifiche.

>[!tip] Testing guidato dagli scenari d'uso
>È spesso possibili derivare i casi di test dalla specifica degli scenari d'uso. Per ogni caso si possono elencare tutti i possibili ingressi che lo caratterizzano e provare quindi il comportamento del programma a fronte di tali casi.

>[!tip] Derivazione (semi)automatica dei casi di test dalle specifiche
>Esistono linguaggi di specifica da cui si riesce a generare in modo (semi)automatico casi di test, in questo caso il testing è più efficace e automatizzato.
>
>Generalmente queste specifiche permettono lo sviluppo di tool per la generazione automatica di casi di test (eventualmente anche con i risultati attesi).

>[!tip] Testing guidato dai casi limite
>Alcuni errori tipici si manifestano in prossimità dei confini delle classi di equivalenza (definite come input che producono lo stesso output). Tra i vari casi di test è dunque opportuno, soprattutto nel Black-box testing, introdurre dei dati di test che vadano a verificare una corretta implementazione per i casi limite.

### Grafi causa effetto
>[!note]
>I grafi causa effetto sono il modo più comune di determinare un insieme minimo di casi di test. Questi grafi mettono in relazione fatti elementari (booleani) con i risultati attesi (sempre booleani).
>
>L'idea è che conoscendo la dipendenza di un risultato dalla combinazione degli ingressi potremo stimolare il sistema esattamente con tale combinazione e verificare se il risultato reale coincide con quello atteso.

Talvolta risulta conveniente passare da tabelle organizzate in questo modo:
![[Pasted image 20251125153841.png|center]]