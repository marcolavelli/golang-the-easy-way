# Golang The Italian Easy Way
Traduzione, approfondimento e semplificazione in lingua italiana della Guida ufficiale *Go*

# Introduzione
Prima di iniziare, se non l'hai già fatto, installa *Go* => https://go.dev/doc/install

Apri un prompt dei comandi e crea una directory progetto per il primo codice sorgente *Go*
>     mkdir progetto
>     cd progetto

Abilita il monitoraggio delle dipendenze: crea un file go.mod e assegna il nome del modulo in cui si troverà il codice
>     go mod init ciao.go/progetto

Crea un file *ciao.go* e verifica la struttura del progetto
>       └── progetto
>           ├── ciao.go
>           └── go.mod

Apri l'editor di testo e scrivi il seguente codice
>       package main
>       import "fmt"
>       func main() {
>           fmt.Println("Ciao, Mondo!")
>       }

Esegui il codice per vedere il saluto
>       go run .

Fantastico! Hai creato il primo programma e ora sei pronto a vivere una magica avventura nel mondo di *Go* 

# Pacchetti
Ogni programma *Go* è composto da pacchetti e inizia ad essere eseguito nel pacchetto *main*
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

Se due o più parametri consecutivi sono dello stesso tipo è possibile ometterlo da tutti tranne l'ultimo
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

# Tipi di base
I tipi di base in *Go* suddivisi per dimensione sono
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

Il tipo *int* è consigliato per un valore intero e, come per i tipi *uint* e *uintptr*, la sua dimensione dipende dall'architettura della macchina

In *Go* ci sono anche due alias, il tipo *byte* che equivale a *uint8* e il tipo *rune* che vale *int32*

Le variabili possono essere dichiare senza un valore esplicito e viene assegnato a loro il valore *zero*, differente a seconda del tipo
>     var numerico int          =>  numerico = 0
>     var booleano bool         =>  booleano = false
>     var vocabolo string       =>  vocabolo = ""  

# Conversione di tipo
L'espressione *T(v)* converte il valore *v* nel tipo *T*
>     var i int = 271
>     var f float64 = float64(i) / 100

A differenza di *C*, in *Go* l'assegnazione tra elementi di tipo diverso richiede una conversione esplicita

# Costanti
Le costanti sono dichiarate come le variabili ma con la parola chiave *const* e il loro nome inizia com la prima lettera maiuscola
>     const Pi = 3.14

Le costanti non possono essere dichiarate utilizzando l'assegnazione breve *:=*

# For
*Go* ha un solo costrutto di loop, il ciclo *for*
>     for i := 0; i < 10; i++ {
>         fmt.Println(i)
>     }
    
Il ciclo *for* di base ha tre componenti, non obbligatorie, separate da punto e virgola
- *init* : la dichiarazione iniziale di variabili visibili nell'ambito del ciclo
- *cond* : l'espressione di condizione valutata prima di ogni iterazione
- *post* : l'istruzione eseguita alla fine di ogni iterazione

Se ometti le istruzioni *init* e *post*, si possono togliere i punti e virgola e il ciclo *for* diventa come un ciclo *while* di *C*
>     i := 1
>     for i < 10 {
>         i += i
>     }

Se ometti la condizione di ciclo *cond* si ottiene un *loop infinito*, con o senza *init* e *post*
>     for {
>     } 

>     for i := 0; ; i++ {
>         fmt.Println(i)
>     } 
