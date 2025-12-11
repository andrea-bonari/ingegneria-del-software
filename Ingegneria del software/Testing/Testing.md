>[!note]
>Il testing è il collaudo dei programmi, e si applica al risultato dello sviluppo, cioè agli eseguibile. Ha lo scopo di far emergere quanti più difetti possibile.

Per comprendere quali sono i momenti in cui si fa testing e gli obiettivi di ciascuna fase si introduce il modello a V:
![[Pasted image 20251125150646.png|center]]
I vari livelli del testing si riferiscono all'oggetto del testing, cioè la fase del ciclo di vita che prodotto il programma che viene testato. Possibili oggetti di testing possono essere moduli, sottosistemi e interi sistemi.

>[!tip] Test di unità
>Il test di unità (o modulo) si riferisce al più piccolo elemento costitutivo di un sistema. Generalmente è prodotto da un solo programmatore o da un piccolo team. È generalmente eseguito dal programmatore stesso prima del rilascio, e i test che vengono effettuati sono ideati dal programmatore stesso.

>[!tip] Test di integrazione
>Il test di integrazione si riferisce ad un insieme di componenti che devono essere integrati per formare il sistema. Viene effettuato da un gruppo di testing apposito, di cui tipicamente non fanno parte i programmatori.
>
>Le interfacce da verificare sono indicate dai documenti di progetto del sistema.

>[!tip] Test delle interfacce
>Nel test delle interfacce si usa un driver (simulatore del modulo che inizia l'interazione) per sollecitare le interfacce di un altro modulo, per verificare tutti gli interscambi tra moduli. I moduli sotto esame possono usare a loro volta dei moduli stub, cioè dei simulatori dei moduli eventualmente utilizzati.
>
>Generalmente si verifica un interfaccia per volta, procedendo in modo incrementale.

>[!tip] Test di sistema
>Nel test di sistema è necessario verificare il corretto funzionamento del software tramite verifica e validazione. A seconda dello scopo il test di sistema si distingue tra test di sistema propriamente detto e test di accettazione.
>
>A volte non esiste un committente quindi non esiste un test di accettazione. In questo caso si ricorre al beta-test.

>[!tip] Test di regressione
>Generalmente quando si rilascia una nuova versione dello stesso programma si verifica che le caratteristiche pienamente soddisfacenti nella versione precedente non siano state compromesse.

### Processo di testing 
>[!note]
>Data la situazione, il programma $P$ elabora dati di ingresso appartenenti ad un insieme $I$ e produce risultati appartenenti all'insieme $O$, effettuare il test vuol dire selezionare un sottoinsieme $T\subseteq I$, ed eseguire $P$ per ogni $t\in T$.
>
>I casi di test sono dati dalle coppie $(\text{dato di test}, \text{ risultato atteso})$. Ovviamente dopo aver eseguito $P$ con ingresso $t$ occorre confrontare il risultato ottenuto con quello previsto.
>
>Occorre un processo di test che inizi dal design dei casi di test in grado di sollecitare il sistema in una gamma di situazioni ampia.
