---
layout: default
---

## Perchè Docker?

Docker ha rivoluzionato il modo di sviluppare e distribuire software, introducendo il concetto di **container applicativo.**  
Questo termine, si riferisce ad uno specifico modello di conteinerizzazione che possiamo sintetizzare usando 3 parole chiave: **Build, Ship e Run.**

### Build

Il termine Build, indica la tecnica con cui si definiscono tutte le componenti necessarie per l’esecuzione di un processo applicativo. Questo raggruppamento di file, a partire dal sistema operativo e dalle librerie di base, descrive quella che in Docker si chiama **immagine.**

### Ship

Il processo di Build, basato sulla scrittura di un file di testo, il **Dockerfile**, rende possibile trattare le immagini Docker nello stesso modo in cui gestiamo già il codice applicativo. Ad esempio, possiamo caricare il codice in un repository Git, per il versionamento e la condivisione. Questo è proprio ciò che significa il termine Ship, trovare un formato standard per **semplificare la distribuzione** delle nostre applicazioni.

### Run

Il terzo termine, Run, è in realtà il primo che ha direttamente a che vedere con il concetto di container. E’ infatti in questa fase che, sulla base di un’immagine Docker, viene creato un nuovo “root file system”, il **container** appunto. Oltre allo spazio disco, così realizzato e a questo punto modificabile, ogni container ha ovviamente anche i suoi processi, la sua memoria, il suo stack di rete.

E’ Docker, in particolare il componente Docker Engine, che si occupa di creare tutto ciò per eseguire la nostra applicazione. Lo fa, utilizzando le risorse dell’host, locale o in cloud, su cui è in esecuzione.

Il Docker Engine può essere configurato su differenti piattaforme, seguendo la [guida ufficiale](https://docs.docker.com/engine/getstarted/step_one/){:target="_blank"} di Docker.

## Sviluppare con Docker

Terminata l'installazione del Docker Engine e degli strumenti client, è ora di iniziare ad usare Docker!

Come cambia lo sviluppo della nostra applicazione con Docker?  
Docker sicuramente introduce nuovi strumenti legati al pattern Build-Ship-Run però, il cuore della nostra applicazione resta assolutamente il nostro codice applicativo, scritto con uno dei numerosi linguaggi di programmazione.  
In questo senso, non dobbiamo considerare Docker come una tecnologia invasiva che cambia la nostra applicazione o il modo in cui scriviamo il suo codice.

### Applicazione di esempio

Come tutti i corsi introduttivi, anche questo propone un'applicazione "Hello World" di esempio.  
La scelta del linguaggio di programmazione è ricaduta su [Golang](https://it.wikipedia.org/wiki/Go_(linguaggio_di_programmazione)){:target="_blank"}, per la sua chiarezza e leggibilità. Naturalmente, i concetti che verranno presentati si potranno applicare anche agli altri linguaggi di programmazione più diffusi.

Il codice dell'applicazione di esempio corrisponde al file [main.go](https://github.com/LOG-ED/docker-get-started/blob/master/main.go){:target="_blank"} presente nella root del nostro repository.

### Docker e Golang

Se fossimo dei programmatori Go probabilmente avremmo già installato e configurato il compilatore di Go in locale, 
ma per chi non conosce questo linguaggio di programmazione o non lo ha mai utilizzato, vedremo come compilare la nostra applicazione Go senza installare appunto alcuno strumento specifico di questo linguaggio.
Per fare ciò, utilizzeremo una immagine di Docker che incorpora al meglio tutti gli strumenti necessari.
Si tratta dell'immagine Docker [ufficiale per Golang](https://hub.docker.com/_/golang/){:target="_blank"} depositata sul Docker Hub, che è uno dei principali archivi di immagini pubbliche.

Per utilizzare l'immagine di Golang dobbiamo prima scaricarla in locale, dove è in esecuzione il Docker Engine. Ad esempio con questo comando che deve essere eseguito da terminale:

```$ docker pull golang```

Eseguendo il comando si avvierà il processo di download dell'immagine con la classica indicazione sull'avanzamento.

### Il primo container

Terminato il processo di scaricamento dell'immagine, possiamo utilizzarla direttamente per la compilazione della nostra applicazione di esempio. In che modo? Ricordate il termine Run? E' la fase in cui a partire da un'immagine di base, ad esempio golang, viene creato un nuovo container con un proprio file system in cui troveremo pronti all'uso, tutti gli strumenti per la compilazione e l'esecuzione della nostra applicazione di esempio.  
Per il run del nostro primo container apriamo il terminale e spostiamoci nella directory dove è presente il file main.go. A questo punto eseguiamo questo comando da terminale:

```$ docker run --rm -v "$PWD":/go/src/helloworld golang go run /go/src/helloworld/main.go```

Il risultato che ci attendiamo è la stampa a terminale della frase "Hello World".

### Cosa è successo?

Se non avete avuto errori, come ci attendevamo, è stato creato temporaneamente un nuovo container che è stato utilizzato per compilare ed eseguire la nostra applicazione di esempio. Se tutti gli strumenti di Go erano già inclusi nella immagine Docker di base, dove è stato preso il sorgente dell'applicazione?  

Il comando run che abbiamo eseguito utilizza i parametri:

| Parametro | Descrizione |
| ------------- |-------------| 
| `-v "$PWD":/go/src/helloworld` | per "mappare" la directory corrente dell'host con la directory "/go/src/helloworld" del container | 
| `go run /go/src/helloworld/main.go` | per compilare l'applicazione in una directory temporanea del container e quindi eseguirla |
| `--rm` | per cancellare il container una volta terminato il comando indicato |
