>[!note]
>Il paradigma funzionale si basa sulle funzioni. Non esiste il concetto di stato o variabile, i dati sono considerati immutabili, mentre una computazione è espressa mediante una trasformazione di dati. In questo paradigma si favorisce la composizione di funzioni.
>
>In Java questo è ottenuto tramite le espressioni lambda, cioè funzioni anonime usate per esprimere implementazioni concisamente, in combinazione con le interfacce funzionali (interfaccia con un unico metodo e sintassi semplificata per l'implementazione). La loro sintassi è:
>```java
>(parametri) -> espressione
>```

Di base java fornisce alcune interfacce funzionali, tra cui:
- `Function<T,R>`
- `BiFunction<T,U,R>`
- `Consumer<T>` (nessun valore di ritorno)
- `Predicate<T>` (valore di ritorno booleano)

>[!tip] Riferimenti al metodo
>Spesso le espressioni lambda vengono utilizzate per richiamare un metodo già esistente, in questi casi Java offre una sintassi di riferimento al metodo, formato da: `<oggetto o classe>::<nome del metodo>`
### Optional
>[!note]
>`Optional<T>` è una classe che incapsula un valore che può essere presente o assente, eliminando la necessità di utilizzare i valori `null`. Grazie a questo meccanismo si aumenta la leggibilità del codice e si previene più facilmente errori come `NullPointerException`.

I metodi principali di `Optional<T>` sono:
- `Optional.of()`: metodo statico che crea un `Optional` per un oggetto non nullo.
- `Optional.empty()`: metodo statico che restituisce un oggetto `Optional` empty.
- `Optional.ofNullable()`: metodo statico che crea un `Optional` per un oggetto che può essere nullo, nel caso restituendo un oggetto `Optional.empty()`.
- `o.get()`
- `o.ifPresent(Consumer<T> f)`: prende in ingresso un'implementazione di un interfaccia funzionale e ci fa qualcosa, solo se non è vuoto.
- `o.flatMap(Function<T, Optional<U>> f)`: prende in ingresso un'implementazione di un interfaccia funzionale da `T` a `Optional<U>`. Se l'oggetto è empty allora viene propagato, in alternativa la funzione viene applicata al contenuto dell'oggetto.
- `o.orElse(T val)`: prende un valore `Optional<T>` e se non è vuoto ritorna il suo valore, altrimenti ritorna `val`.

Un esempio di codice funzionale con `Optional` può essere:
```java
Optional<Persona> o = ...;
String commenti = o
	.flatMap(p -> p.getIndirizzo())
	.flatMap(i -> i.getCommenti())
	.orElse("no comment");
	
System.out.println(commenti);
```

### Stream
>[!note]
>`Stream<T>` è una rappresentazione immutabile di una collection, permette di vedere un flusso di oggetti di tipo `T` contenuti in essa. Partendo da una `Collection<T>` il metodo `.stream()` la trasforma in una stream, che nasconde la molteplicità degli elementi e contiene numerosi metodi per trasformare uno stream in un altro stream

Di seguito i metodi principali di `Stream<T>`:
- `void forEach(Consumer<T> c)`: itera attraverso tutti gli elementi dello stream, applicando un'operazione `c` a ciascun elemento.
- `Stream<T> filter(Predicate<T> p)`: filtra i dati contenuti nello stream iniziale sulla base del predicate `p` di input: solo gli elementi che soddisfano il predicato sono aggiunti nello Stream risultante.
- `Stream<U> map(Function<T,U> f)`: trasforma tutti gli elementi dello stream iniziale tramite la `Function<T,U>` di input. Si ottiene un nuovo `Stream<U>` composto dagli elementi trasformati.
- `Stream<T> distinct()`: elimina i duplicati (`a` e `b` sono duplicati se `a.equals(b)`).
- `Stream<T> sorted(Comparator<T> c)`: ordina gli elementi. Nel caso di interi e stringhe il comparator `c` non è necessario e si applica l'ordinamento naturale.
- `Stream<U> flatMap(Function<T,Stream<U>> f)`: applica la funzione in ingresso a tutti gli elementi dello Stream iniziale, generando uno "Stream di Stream". Successivamente, "appiattisce" lo Stream di Stream in un unico Stream: inserisce in quest'ultimo tutti gli elementi degli Stream di Stream.
- `IntStream mapToInt()`: permette di creare un `IntStream`, è analogo a `mapToDouble()`.
- `U reduce(U base, BiFunction<T, U, U> f)`: operazione che permette di raccogliere un solo valore a partire da uno stream, dove `base` è un valore iniziale mentre `f` è una funzione che prende un risultato parziale e un elemento `U` e mostra come l'elemento si aggiunge al risultato parziale.
- `R collect(Supplier<R> supplier, BiCOnsumer<R, ? super T> accumulator, BiConsumer<R, R> combiner)`: operazione che modifica sempre lo stesso valore, dove `supplier` crea il valore di ritorno, `accumulator` incorpora un elemento nel valore di ritorno e `combiner` combina i due risultati parziali.

>[!tip] Closures
>Supponiamo di avere una funzione lambda che vogliamo usare più volte. È possibile generalizzare, cioè passare come parametro una costante, per esempio un metodo che ritorna una funzione di filtro rispetto ad un certo valore.
>```java
>public static Predicate<String> pred(String prefix) {
>	return s -> s.startsWith(prefix);
>}
>
>list.stream().filter(pred("X"));
>```
>
>Java però impone dei vincoli riguardo le Closures, cioè che una variabile usata in esse non deve mai cambiare dal momento di definizione, rendendola effectively final.

>[!tip] Parallel
>In caso in cui gli elementi di uno stream siano indipendenti tra loro, Java permette di analizzare gli elementi di uno stream in parallelo invocando `parallel()`.
>
>Non è consigliato in situazioni in cui le operazioni condivise coinvolgono risorse condivise non thread-safe, come per esempio nelle operazioni I/O.
>
>Inoltre quando il calcolo è troppo leggero l'overhead di `parallel()` potrebbe rendere l'operazione più lenta.


