>[!note]
>Quando estendiamo una classe, si eredita la sua specifica. Dobbiamo distinguere due scenari principali:
>- Estensioni pure: che non modificano i contratti esistenti.
>- Estensioni non pure: modificano i contratti esistenti.

### Estensioni pure
>[!note]
>Un'estensione si dice pura se non modifica la specifica formale di nessuno dei metodi ereditati. In questo scenario, la sottoclasse può fare due cose:
>- Aggiungere nuovi metodi
>- Eseguire override modificando l'implementazione, ma lasciando intatto il contratto.

In questo caso le funzioni astratte rimangono le stesse, tuttavia le invarianti cambiano quasi sempre, infatti di base l'RI della sottoclasse eredita quello della superclasse e lo rafforza:
```
//@ public invariant \old(RI_super) && nuovo_vincolo;
```

### Estensioni non pure
>[!note]
>Un estensione si dice non pura quando modifica la specifica dei metodi ereditati, e quindi c'è un cambiamento di contratto.
>
>Affinché l'estensione sia valida e non "rompa" il codice che usa la superclasse è necessario usare il principio di sostituzione di Liskov (LSP)

>[!tip] Regole dell'LSP
>Per garantire l'LSP è necessario seguire tre regole fondamentali riguardanti signature, metodi e proprietà.
>
>La regola della signature è garantita dal compilatore Java: i metodi della sottoclasse devono essere compatibili a livello di firma con quelli della superclasse, con l'eccezione che la sottoclasse restituisca un tipo più specifico rispetto alla superclasse.
>
>La regola dei metodi riguarda precondizioni e postcondizioni. Le precondizioni possono solamente essere indebolite, mentre le postcondizioni possono essere solamente rafforzate.
>
>La regola delle proprietà riguarda le proprietà astratte del supertipo, e stabilisce che queste devono essere tutte preservate.

