>[!note]
>Con test di integrazione si intendono test di sistemi o sottosistemi composti, generalmente di tipo black-box. Sono molto critici, poiché generalmente la maggior parte degli errori sono di integrazione.

>[!tip]
>L'integrazione si riferisce generalmente ad una gerarchia di componenti, determinata dalle relazioni di utilizzo.

Per poter testare un certo modulo $A$ talvolta è necessario che $B$ sia disponibile, e se non lo è si ricorre a uno stub. Viceversa, per testare il modulo $B$ occorre che $A$ sia disponibile, e se non lo è si ricorre a un driver.

>[!tip] Strategia "Big bang"
>Questa strategia consiste nell'integrare tutti i componenti in una volta, e rende il testing particolarmente difficoltoso.

>[!tip] Strategia di test incrementale
>Questa strategia consiste nel non integrare tutti i moduli assieme, ma procedendo integrandone un numero progressivamente maggiore. Si può procedere sia con un approccio top-down che bottom-up.
>
>Nell'approccio bottom-up si sviluppano prima i moduli di più basso livello, e si testano con i driver necessari, poi si procede verso l'alto ripetendo il processo.
>
>Nell'approccio top-down si sviluppa e testa il modulo più di alto livello, usando degli stub. Si sviluppano poi i moduli stub e si testano integrati col modulo di massimo livello, usando ulteriori stub per il livello successivo..

### Test delle interfacce
>[!note]
>Il test delle interfacce avviene quando si integrano più moduli (o sottosistemi) per produrre sistemi più ampi. Sono analizzati i parametri passati da un modulo all'altro, la memoria condivisa, le procedure chiamate e la richiesta di servizi tra moduli.

