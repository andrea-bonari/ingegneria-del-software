>[!note]
>L'ingegneria del software è la disciplina che si occupa dello sviluppo, della progettazione, della messa in opera e della manutenzione dei sistemi informatici, applicando metodi e tecniche ingegneristiche per garantire la qualità, la sicurezza e l'efficienza del software. 
>
>Essa fornisce un approccio sistemico e strutturato allo sviluppo di software, con l'obiettivo di creare soluzioni efficienti e cost-effective che soddisfino le esigenze degli utenti, dandoci anche dei metodi tecnici e manageriali per prevedere e tenere sotto controllo i costi per tutta la vita (lifecycle) dei prodotti software.

### Lifecycle del software
>[!note]
>Il ciclo di vita di un prodotto software si riferisce alle diverse fasi attraverso le quali il prodotto passa dal suo concepimento alla sua fine di vita. Esistono diversi modelli per il lifecycle del software.

I cicli di vita cercano di fronteggiare l'evoluzione del software, che non è necessariamente lineare. Non vi è un ciclo di vita usato da tutti, è una scelta fatta in base all'ambito dalle singole aziende.
### Modello a cascata
>[!note]
>Il modello a cascata di Royce è un approccio alla gestione del ciclo di vita dei sistemi software che prevede la sequenziale esecuzione delle fasi di sviluppo, partendo dallo studio della fattibilità e arrivando alla messa in opera e alla manutenzione. Questo modello si basa su una visione lineare e progressiva del processo di sviluppo, con un'attenzione particolare allo scambio di informazioni tra le fasi successive.
>
>In sequenza, il processo di sviluppo copre, lo studio della fattibilità, l'analisi e specifica dei requisiti, la progettazione, l'implementazione e il test di unità, l'integrazione e il test di sistema, la messa in opera e infine la manutenzione.

Questo modello non anticipa però il cambiamento della specifica, lo subisce, e pertanto non è adatto all'uso.

### Modelli AGILE
>[!note]
>I modelli AGILE hanno un approccio alla gestione del ciclo di vita del software che si basa sull'adattarsi ai cambiamenti, e procedere in maniera incrementale. I più noti modelli che adottano questo sistema sono SCRUM e Extreme Programming.

>[!tip] SCRUM
>SCRUM usa una metodologia iterativa e incrementale, parte dal riconoscimento che i committenti possono cambiare idea e che il processo a cascata non è in grado di reggere questa turbolenza.
>
>In SCRUM sono presenti 3 ruoli: lo SCRUM master (responsabile), i product owners (stakeholders), e il team (un piccolo gruppo di generalmente 4-8 persone responsabili dell'analisi, progettazione, implementazione e testing).
>
>Il progetto è organizzato in sprint, cioè periodi da 4 a 7 settimane nella quale si crea un incremento di prodotto rilasciabile (anche parte di un sistema più grande). La funzionalità dello sprint è scelta da un product backlog del progetto nel quale le funzionalità sono marcate da una priorità dei relativi requisiti. Durante lo sprint il backlog è immutabile, e al suo termine i requisiti non soddisfatti tornano nel backlog.
>
>![[Pasted image 20250915150452.png|center]]

>[!tip] Extreme Programming
>L'Extreme Programming (XP) è un approccio alla gestione del ciclo di vita dei sistemi software che si concentra sulla realizzazione di soluzioni software a breve termine, con l'obiettivo di ridurre il "time to market". Questo modello si basa sulla premessa che il software non può essere completamente pre-specificato e quindi richiede una grande flessibilità e adattabilità durante lo sviluppo.
>
>Come SCRUM rivendica la centralità del codice rispetto ad altri artefatti, integrando il testing nel processo come attività centrale. Inoltre fa uso del pair programming, una tecnica dove ogni lavoro di implementazione è fatta da due programmatori.
>
>In questo metodo il refactoring è continuo. Pertanto è utilizzato per realizzare prototipi per valutare le esigenze degli utenti e migliorare la soluzione. Se il prototipo non è accettato può essere buttato via e riprogettato.

### Modello DevOps
>[!note]
>Il DevOps (Development and Operations) è un approccio alla gestione dei sistemi informatici che combina la fase di sviluppo (Dev) e la fase di operazione (Ops). L'obiettivo principale del DevOps è ridurre il tempo di reazione alle richieste degli utenti, migliorare la qualità del software e aumentare l'efficienza dei processi di produzione.
>
>Il DevOps si concentra sulla collaborazione tra gli sviluppatori (Dev) e le squadre di operazioni (Ops), per creare un flusso di lavoro continuo e automatico che permetta di rilasciare software di alta qualità in tempi rapidi, utilizzando sistemi come CI/CD (Continuous Integration/Continuous Delivery).
