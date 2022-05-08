# Guida galattica per autostoppisti Gopheriani
Guida galattica per autostoppisti Gopheriani (traduzione e sintesi italiana della Guida ufficiale https://go.dev/)

# Installazione
Per installare Go seguire le istruzioni ufficiali https://go.dev/doc/install

# Inizio
Il primo passo è creare una nuova directory per il progetto
>     mkdir progetto
>     cd progetto

in seguito creare un go.mod file per gestire le dipendenze
>     go mod init programma.go/progetto

infine creare il file Go indicato in precedenza
>     touch programma.go

# Pacchetti
Ogni programma Go è composto da pacchetti

I programmi iniziano ad essere eseguiti nel pacchetto main
>     package main

Per convenzione il nome del pacchetto è lo stesso dell'ultimo elemento del percorso di importazione
>     import ("math/rand")
>     rand.Intn(10)

L'ambiente in cui vengono eseguiti i programmi è deterministico, quindi ogni volta che si esegue rand.Intn restituirà lo stesso numero; per vedere un numero diverso si deve seminare il generatore di numeri
>     rand.Seed(time.Now().UTC().UnixNano())

# Importazioni
Possiamo scrivere più istruzioni di importazioni
>     import "fmt
>     import "math/rand"

ma è buon stile di programmazione usare l'istruzione fattorizzata
>     import (
>       "fmt"
>       "math/rand"
>     )

# Nomi esportati
In Go un nome è esportato se inizia con una lettera maiuscola
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
