# gonotes
Guida galattica per autostoppisti Gopheriani (traduzione italiana e sintesi della Guida ufficiale https://go.dev/)	

# inizio
Il primo passo è creare una nuova directory per il progetto
>     mkdir progetto
>     cd progetto

In seguito creare un go.mod file per gestire le dipendenze
>     go mod init programma.go/progetto

Ed infine creare il file Go indicato precendentemente
>     touch programma.go

# pacchetti
Ogni programma Go è composto da pacchetti

I programmi inziano ad essere eseguiti nel pacchetto main
>     package main

Per convenzione il nome del pacchetto è lo stesso dell'ultimo elemento del percorso di importazione
>     import ("math/rand")
>     rand.Intn(10)

L'ambiente in cui vengono eseguiti i programmi è deterministico, quindi ogni volta che si esegue rand.Intn restituirà lo stesso numero

Per vedere un numero diverso si deve seminare il generatore di numeri
>     rand.Seed(time.Now().UTC().UnixNano())

# importazioni
Possiamo scrivere più istruzioni di importazioni
>     import "fmt
>     import "math/rand"

ma è buon stile di programmazione usare l'istruzione fattorizzata
>     import (
>       "fmt"
>       "math/rand"
>     )

  
