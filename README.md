# Guida galattica per autostoppisti Gopheriani
Guida galattica per autostoppisti Gopheriani (traduzione italiana e sintesi della Guida ufficiale https://go.dev/)

# Installazione
Per installare Go seguire le istruzioni ufficiali https://go.dev/doc/install

# Inizio
Il primo passo è creare una nuova directory per il progetto
>     mkdir progetto
>     cd progetto

In seguito creare un go.mod file per gestire le dipendenze
>     go mod init programma.go/progetto

Ed infine creare il file Go indicato in precedenza
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
In Go, un nome viene esportato se inizia con una lettera maiuscola
>     math.Pi

