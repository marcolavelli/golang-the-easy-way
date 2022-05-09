# Guida galattica per autostoppisti Gopheriani
Guida galattica per autostoppisti Gopheriani (traduzione e sintesi italiana della Guida ufficiale => https://go.dev/)

# Installazione
Per installare Go seguire le istruzioni ufficiali => https://go.dev/doc/install

# Inizializzazione
Il primo passo di un programma Go è creare una directory per il progetto
>     mkdir progetto
>     cd progetto

il secondo è creare un *go.mod* file per la gestione delle dipendenze
>     go mod init programma.go/progetto

e per ultimo creare il file Go, indicato in precedenza
>     touch programma.go

Happy coding!

# Pacchetti
Ogni programma Go è composto da pacchetti ed inizia ad essere eseguito nel pacchetto *main*
>     package main

Per convenzione il nome del pacchetto è lo stesso dell'ultimo elemento del percorso di importazione
>     import ("math/rand")
>     rand.Intn(10)

L'ambiente in cui vengono eseguiti i programmi è deterministico, quindi ogni volta che si esegue rand.Intn restituirà lo stesso numero; per vedere un numero diverso si deve "seminare" il generatore di numeri
>     rand.Seed(time.Now().UTC().UnixNano())

# Importazioni
In Go possiamo scrivere più istruzioni di importazioni
>     import "fmt
>     import "math/rand"

ma è buon stile di programmazione usare l'istruzione fattorizzata
>     import (
>       "fmt"
>       "math/rand"
>     )

Un nome "esportato" inizia con una lettera maiuscola
>     math.Pi

# Funzioni
Una funzione può accettare zero o più parametri
>     func add(x int, y int) int { ...

Si noti che il tipo viene dopo il nome della variabile

Se due o più parametri consecutivi sono dello stesso tipo è possibile ometterlo da tutti tranne l'ultimo
>     func add(x, y int) int { ...

Una funzione può restituire un numero qualsiasi di risultati
>     func swap(x, y int) (int, int) {
>         return y, x
>     }

Una funzione può avere valori di ritorno "denominati" e restituirli con un'istruzione return senza argomenti
>     func split(sum int) (x, y int) {
>         x = sum * 4 / 9
>         y = sum - x
>         return
>     }

Questa istruzione è nota come "ritorno nudo", e dovrebbe essere utilizzata solo in funzioni brevi

# Variabili
L'istruzione *var* dichiara un elenco di variabili e, come negli elenchi di argomenti delle funzioni, il tipo è l'ultimo
>     var c, python, java bool

Una dichiarazione var può includere inizializzatori, uno per variabile, e il tipo può essere omesso
>     var c, python, java = true, false, "no!"

L'assegnazione breve *:=* può sostituire una dichiarazione *var* con tipo implicito ma solo all'interno di una funzione
>     func main() {
>         c, python, java := true, false, "no!"
>         ...

# Tipi di base
I tipi di base in Go suddivisi per dimensione sono
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

Il tipo *int* è consigliato per un valore intero e, come per i tipi *uint* e *uintptr*, la sua dimensione dipende dalla piattaforma (32 o 64 bit)

In Go ci sono anche due alias, il tipo *byte* che equivale a *uint8* e il tipo *rune* che vale *int32*
