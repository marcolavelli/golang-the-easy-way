# Guida galattica per autostoppisti Gopheriani
Guida galattica per autostoppisti Gopheriani (traduzione e sintesi italiana della Guida ufficiale => https://go.dev/)

# Installazione
Per installare Go seguire le istruzioni ufficiali => https://go.dev/doc/install

# Inizio
Il primo passo è creare una directory per il nuovo progetto
>     mkdir progetto
>     cd progetto

il secondo è creare un go.mod file per la gestione delle dipendenze
>     go mod init programma.go/progetto

ed infine creare il file Go
>     touch programma.go


# Pacchetti
Ogni programma Go è composto da pacchetti

I programmi iniziano ad essere eseguiti nel pacchetto main
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

Una dichiarazione var può includere inizializzatori, uno per variabile
>     var c, python, java = true, false, "no!"

Se è presente un inizializzatore, il tipo può essere omesso e la variabile prenderà il tipo dell'inizializzatore

All'interno di una funzione, l'istruzione di assegnazione breve *:=* può essere utilizzata al posto di una dichiarazione *var* con tipo implicito
>     func main() {
>         c, python, java = true, false, "no!"
>         ...
