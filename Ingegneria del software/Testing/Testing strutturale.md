>[!note]
>Il testing strutturale, al contrario del testing black-box tiene conto della struttura interna del programma, e quindi i casi di test sono derivati da un'analisi diretta dell'implementazione.
>
>L'obiettivo di questo test è sollecitare tutte le parti del programma, tuttavia applicare questo criterio in modo esaustivo è generalmente molto costoso o infattibile, infatti si fa solo su porzioni particolarmente critiche del codice.

L'insieme dei casi di test deve essere selezionato in modo che ogni istruzione del codice venga eseguita almeno una volta, per esempio nel codice:
```c
int sqrt(int n) {
	int i = 1, z = 1;
	
	if(n < 0)
		return -1;
	
	while(z <= n) {
		i++;
		z = i*i;
	}
	
	return i - 1;
}
```

Sono scelti casi con $n<0$ e $n>0$.

>[!tip] Criterio di Edge Coverage
>L'insieme dei casi di test dev'essere definito in modo che ogni ramo del "Control Flow Graph" del programma venga attraversato almeno una volta.
>
>Per applicare tale criterio è necessario quindi costruire il Control Flow Graph, che rappresenta il flusso di controllo del programma da testare con una certa approssimazione.

>[!tip] Criterio di copertura delle decisioni e delle condizioni
>Con questo criterio l'insieme dei casi di test dev'essere definito in modo che ogni ramo del CFG venga attraversato almeno una volta e con tutti i possibili valori sottoespressioni che compaiono nelle condizioni compose, per esempio:
>```c
>void p(int x, int y) {
>	if(x == 0 || y > 0) {
>		y = y / x;
>	} else {
>		y = (-y) / x;
>	}
>}
>```
>
>I casi di test $(x=0,y=-1)$, $(x=1,y=1)$ e $(x=1,y=-1)$ soddisfano il criterio ed individuano il rischio di divisione per $0$ nel ramo `then`.

>[!tip] Criterio di copertura dei cammini
>Con questo criterio l'insieme dei casi di test deve garantire che ogni possibile cammino che porti dal nodo iniziale al nodo finale del CFG sia percorso una o anche più volte.
>
>In generale il numero di casi di test richiesti è troppo elevato per poter essere applicato in pratica.

