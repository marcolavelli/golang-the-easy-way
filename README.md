# Golang 🦫 The Easy Way
Guida sintetica e semplice del linguaggio *Go* (prima edizione in lingua italiana)

# Introduzione
Prima di iniziare, se non l'hai già fatto, installa *Go* => https://go.dev/doc/install

Apri un prompt dei comandi e crea una directory *progetto* per il tuo primo codice sorgente *Go*
>     mkdir progetto
>     cd progetto

Abilita il monitoraggio delle dipendenze: crea un file *go.mod* e assegna il nome del modulo in cui si troverà il codice
>     go mod init ciao.go/progetto

Crea un file *ciao.go* e verifica la struttura del progetto
>       └── progetto
>           ├── ciao.go
>           └── go.mod

Apri l'editor di testo e scrivi il seguente codice
>       package main
>       
>       import "fmt"
>       
>       func main() {
>           fmt.Println("Ciao, Mondo!")
>       }

Esegui il codice per vedere il saluto
>       go run .

Fantastico! Benvenuto nel mondo dei *Gophers* 

# Pacchetti
Un programma *Go* è composto da pacchetti e la sua esecuzione inizia dal pacchetto *main*
>     package main

Per convenzione il nome del pacchetto è lo stesso dell'ultimo elemento del percorso di importazione
>     import ("math/rand")
>     rand.Intn(10)

L'ambiente in cui vengono eseguiti i programmi è deterministico, quindi ogni volta che si esegue *rand.Intn*, esso restituirà lo stesso numero; per vedere un numero diverso si deve "seminare" il generatore di numeri
>     rand.Seed(time.Now().UTC().UnixNano())

# Importazioni
In *Go* possiamo scrivere più linee di istruzione per le importazioni
>     import "fmt
>     import "math/rand"

ma è buon stile di programmazione usare l'istruzione fattorizzata
>     import (
>       "fmt"
>       "math/rand"
>     )

Un nome "esportato" inizia sempre con una lettera maiuscola
>     math.Pi

# Funzioni
Una funzione può accettare zero o più parametri e può restituire un numero qualsiasi di risultati
>     func swap(x int, y int) (int, int) {
>         return y, x
>     }

Se due o più parametri consecutivi sono dello stesso tipo allora è possibile omettere il tipo da tutti i parametri tranne nell'ultimo
>     func add(x, y int) int {
>         return x + y
>     }   

Una funzione può avere valori di ritorno "denominati" e restituirli con un'istruzione *return* senza argomenti
>     func split(sum int) (x, y int) {
>         x = sum * 4 / 9
>         y = sum - x
>         return
>     }

Questa istruzione è nota come "ritorno nudo", e dovrebbe essere utilizzata solo in funzioni brevi

# Variabili
L'istruzione *var* dichiara un elenco di variabili e, come negli elenchi di argomenti delle funzioni, il tipo viene dopo i nomi delle variabili
>     var c, python, java bool

Una dichiarazione *var* può includere inizializzatori, uno per variabile, e il tipo può essere omesso
>     var c, python, java = true, false, "no!"

L'assegnazione breve *:=* può sostituire una dichiarazione *var* con tipo implicito ma solo all'interno di una funzione
>     func main() {
>         c, python, java := true, false, "no!"
>         ...

Le variabili possono essere dichiarate senza un valore esplicito e viene assegnato a loro il valore *zero*, differente a seconda del tipo
>     var numerico int          // numerico = 0
>     var booleano bool         // booleano = false
>     var vocabolo string       // vocabolo = ""  

# Tipi di base

###### Tabella 1 - Tipi di base in Go suddivisi per dimensione occupata
| size undef | size 08 bit | size 16 bit | size 32 bit | size 64 bit |
| :---------- | :---------- | :---------- | :---------- | :---------- |
| | bool |
| string |
|int | int8 | int16 | int32 | int64 |
|uint | uint8 | uint16 | uint32 | uint64 |
| uintptr |
| | byte |
| | | | rune |
| | | | float32 | float64 |
| | | | complex32 | complex64 |

Il tipo *byte* è equivalente al tipo *uint8* mentre il tipo *rune* al tipo *int32*

Le dimensioni dei tipi *int*, *uint* e *uintptr* dipendono dall'architettura della macchina

# Conversione di tipo
L'espressione *T(v)* converte il valore *v* nel tipo *T*
>     var i int = 271
>     var f float64 = float64(i) / 100

A differenza di *C*, in *Go* l'assegnazione tra elementi di tipo diverso richiede una conversione esplicita

# Costanti
Le costanti sono dichiarate come le variabili ma con la parola chiave *const* e il loro nome inizia con la prima lettera maiuscola
>     const Pi = 3.14

Le costanti non possono essere dichiarate utilizzando l'assegnazione breve *:=*

# For
*Go* ha un solo costrutto di loop, il ciclo *for*
>     for i := 0; i < 10; i++ {
>         fmt.Println(i)
>     }
    
Il ciclo *for* di base ha tre componenti, non obbligatorie, separate da punto e virgola:
- *init* : la dichiarazione iniziale di variabili, visibili nell'ambito del ciclo
- *cond* : l'espressione di condizione valutata prima di ogni iterazione
- *post* : l'istruzione eseguita alla fine di ogni iterazione

Se si omettono le istruzioni *init* e *post*, e i punti e virgola, si ottiene un ciclo *while* di *C*
>     i := 0
>     for i < 10 {
>         i += 1
>     }

Se si omette la condizione di ciclo *cond* si ottiene un *loop infinito*
>     for {
>         // loop infinito
>     } 

# If
*Go* ha un'istruzione *if* che può iniziare con una breve istruzione da eseguire prima della condizione  
>     if x > limit {
>         return limit - 1
>     } else {
>	      return x
>     }     

>     if y := limit - 1; x <= limit {
>         return x
>     } else {
>	      return y
>     }

Le variabili dichiarate all'interno di un'istruzione *if* sono disponibili anche all'interno di uno qualsiasi dei blocchi *else*

# Switch
*Go* ha un'istruzione *switch-case* simile a quella di *C*, *C++*, *Java*, *JavaScript* e *PHP*, tranne per il fatto che *Go* esegue solo il caso selezionato e non tutti i casi che seguono: l'istruzione *break* non è necessaria alla fine di ogni caso in quanto è fornita automaticamente
>     switch os := runtime.GOOS; os {
>     case "darwin":
>         fmt.Println("Go runs on OS X.")
>     case "linux":
>         fmt.Println("Go runs on Linux.")
>     default:
>         fmt.Printf("Go runs on %s.\n", os) // freebsd, openbsd, plan9, windows...
>     }

Un'altra differenza è che i casi previsti possono non essere costanti e i valori possono non essere numeri interi

>     t := time.Now()
>     
>     switch {
>     case t.Hour() < 12:
>	      fmt.Println("Good morning!")
>     case t.Hour() < 17:
>	      fmt.Println("Good afternoon.")
>     default:
>	      fmt.Println("Good evening.")
>     }

L'istruzione *switch* senza una condizione può essere un modo pulito per scrivere lunghe catene *if-then-else*

# Defer
*Go* ha un'istruzione differita *defer* che rinvia l'esecuzione di una funzione fino a quando la funzione circostante non ritorna
>     for i:= 0; i < 10; i++ {
>	      defer fmt.Println(i)
>     }
>     fmt.Println("Print this before the loop and its result will be reversed")

La chiamata di funzione posticipata è inserita in uno stack e viene eseguita in ordine *last-in-first-out*

# Puntatori
*Go* ha un tipo puntatore **T* che contiene l'indirizzo di memoria a un valore *T*
>     var p *int

L'operatore *&* genera un puntatore al suo operando
>     i := 1
>     p = &i

L'operatore * permette di accedere al valore cui il puntatore fa riferimento
>     fmt.Println(*p)
>     *p = 2

Questa istruzione è nota come "dereferenziazione" o "indirizzamento"

# Struct
*Go* ha un tipo *struct* equivalente alla *classe* dei linguaggi basati sulla programmazione orientata agli oggetti
>     type Vertex struct {
>	      X int
>	      Y int
>	  }
>
>     var v = Vertex{1, 2}

I campi di una *struct* sono accessibili tramite un punto *.X* oppure tramite un puntatore *p.X*, senza l'esplicita dereferenza *(*p).X*
>     v.X = 1
>       
>     p := &v
>     p.X = 3

## Struct literals
Le *struct literals* sono utilizzate per creare nuove istanze e l'ordine dei campi è irrilevante
>     v2 := Vertex {Y: 6, X: 4}

# Array
*Go* ha un tipo *array* *[n]T* di dimensione fissa
>     var primes [6]int
>     primes[0] = 2
>     primes[1] = 3
>     primes[2] = 5
>     primes[3] = 7
>     primes[4] = 11
>     primes[5] = 13

La lunghezza *n* fa parte del suo tipo e quindi non può essere ridimensionato

## Array literals
Gli array literals sono utilizzati per creare nuove istanze
>     primes := [6]int{2, 3, 5, 7, 11, 13}

# Slices
*Go* ha un tipo *slice* *[ ]T* di dimensioni dinamiche
>     var threeprimes []int = primes[0:3]

>     fiveprimes := primes[0:5]

Una *slice* è una vista di un *array* e non memorizza i dati, la modifica di un elemento comporta la modifica dell'elemento nell'*array*
>     threeprimes[2] = 0
>     fmt.Println(primes)           // print 2, 3, 0, 7, 11, 13

Anche altre *slices* che condividono lo stesso *array* sottostante vedranno tali modifiche
>     fiveprimes := primes[0:5]
>     fmt.Println(fiveprimes)        // print 2, 3, 0, 7, 11 

## Slice literals
Le *slice literals* sono come *array literals* senza la lunghezza
>     sl := []bool{true, true, false}

## Slice length e capacity
Una *slice* ha sia una lunghezza che una capacità:
- la lunghezza è il numero di elementi che contiene
- la capacità è il numero di elementi nell'*array* sottostante, a partire dal primo elemento della *slice*
>     someprimes := primes[3:]      // len=3 cap=3

Durante lo *slicing* si possono omettere i limiti alto e basso
>     sixprimes[0:6]
>     sixprimes[0:]
>     sixprimes[:6]
>     sixprimes[:]  

La lunghezza di una *slice*, a condizione che abbia una capacità sufficiente, può essere estesa con il *re-slicing* 
>     someprimes = primes[1:5]      // len=4 cap=5
>     someprimes = primes[1:]       // len=5 cap=5
>     fmt.Println(primes)           // print 2, 3, 0, 7, 11, 13

## Nil slice
Il valore zero di una slice è *nil*
>     var noprimes []int                   // len=0 cap=0   

Una *nil slice* ha una lunghezza e capacità uguale a 0 e non ha un *array* sottostante

## Slice built-in
La funzione built-in *make* restituisce una *slice*, inizializzata e pronta per l'uso
>     bestprimes := make([]int, 10)

La funzione built-in *append* è utilizzata per aggiungere elementi ad una *slice* 
>     bestprimes = append(bestprimes, 13)


# Range
*Go* ha un'istruzione *range* per iterare una *slice* o una *map*

Il *ranging* di una *slice* restituisce due valori:
- il primo è l'indice
- il secondo è una copia dell'elemento in quell'indice
>     var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
>     
>     for i, v := range pow {
>         fmt.Printf("2**%d = %d \n", i, v)
>     }

Nell'istruzione *range* si può omettere l'indice o il valore assegnando *_*
>     for i, _ := range pow
>     for _, value := range pow

Se si vuole solo l'indice, si può anche omettere la seconda variabile
>     for i := range pow

# Mappe
*Go* ha un tipo *map* che associa le chiavi ai valori
>     var m map[string]int
>     
## Map literals
Le *map literals* sono come *struct literals* ma le chiavi sono obbligatorie
>     ml := map[string]int{"zero": 0, "uno": 1, "due": 2}

## Nil map
Il valore zero di una mappa è *nil*

Una *nil map* non ha chiavi e non si possono aggiungerne

## Map built-in
La funzione built-in *make* restituisce una *map* del tipo specificato, inizializzata e pronta per l'uso
>     m := make(map[string]int)

La funzione built-in *delete* è utilizzata per eliminare un elemento da una *map*
>     ml := delete("due": 2)

# Funzioni valore
In *Go* una funzione è anche valore e può essere utilizzata come argomento o valore di ritorno

>     var adder := func(x, y float64) float64 {
>         return x + y
>     } 
>     
>     func compute(fn func(float64, float64) float64) float64 {
>         return fn(3, 4)
>     } 
>     
>     fmt.Println(compute(adder))

# Funzioni closure
In *Go* una funzione può essere una *closure*, una funzione valore "vincolata" alle variabili esterne al suo corpo

>     func fibonacci() func() int {
>         a, b := 0, 1
>         return func() int {
>             a, b = b, a+b
>             return a
>         }
>     }
>     
>     func main() {
>         f := fibonacci()
>         fmt.Println(f(), f(), f(), f(), f())
>     }

# Literals
*Go* come altri linguaggi di programmazione usa istruzioni *literal* per dichiarare e inizializzare una struttura di dati:

- 👍 il codice riflette la struttura dei dati
- 👎 il layout deve essere conosciuto in anticipo
- ✍️ il contenuto deve essere inizializzato
>     purpleStruct := {red: 128, green: 0, blue: 128}
>
>     purpleArray := [3]int{128, 0, 128}
>
>     purpleSlice := []int{128, 0, 128}
>
>     purpleMap := map[string]int{"red": 128, "green": 0, "blue": 128} 

