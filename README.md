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
    
Il ciclo *for* di base ha tre componenti, non obbligatorie, separate da punto e virgola
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

Le *struct literals* sono utilizzare per creare nuove istanze e l'ordine dei campi è irrilevante
>     v2 := Vertex {Y: 6, X: 4}

# Array
*Go* ha un tipo array *[n]T* di dimensione fissa
>     var primes [6]int
>     primes[0] = 2
>     primes[1] = 3
>     primes[2] = 5
>     primes[3] = 7
>     primes[4] = 11
>     primes[5] = 13

>     primes := [6]int{2, 3, 5, 7, 11, 13}

La lunghezza *n* fa parte del suo tipo e quindi non può essere ridimensionato

# Slices
*Go* ha un tipo slice *[ ]T* di dimensioni dinamiche degli elementi di un array
>     var threeprimes []int = primes[0:3]

>     sixprimes := primes[0:5]

Una slice è una vista e non memorizza i dati quindi la modifica di un suo elemento comporta la modifica dell'elemento nell'array sottostante
>     threeprimes[2] = 0
>     fmt.Println(primes)           // print 2, 3, 0, 7, 11, 13

Altre slice che condividono lo stesso array sottostante vedranno tali modifiche
>     sixprimes := primes[0:5]
>     fmt.Println(sixprimes)        // print 2, 3, 0, 7, 11 
