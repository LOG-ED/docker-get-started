---
layout: default
---

## Build, Ship e Run

Tra i primissimi concetti descritti, vi ricordate quello di Build-Ship-Run?  
Abbiamo già fatto riferimento, in modo esplicito, al termine Run, perchè corrisponde al comando
che abbiamo utilizzato per creare il nostro primo container. Il termine Build è tra le istruzioni 
che abbiamo trovato nel docker-compose.yml e abbiamo accennato che riguarda la fase di creazione di un'immagine.
E' il momento di parlare del termine Ship.

### Ship

Per creare un container dobbiamo sempre indicare un'immagine di base.  
Le immagini di base possono essere scaricate da un archivio remoto, un registry service per l'esattezza,
come ad esempio il [Docker Hub](https://hub.docker.com/explore/){:target="_blank"} oppure create adhoc,
quando e dove ci servono, per la nostra applicazione.   
Il termine Ship si riferisce al fatto che, in ogni caso, le immagini sono sempre trasferibili da e verso un registry.  
Inoltre, nel momento in cui creiamo la nostra specifica immagine, siamo in grado di sapere esattamente come è fatta
e possiamo trasferire e versionare anche questa informazione.

## Come si crea un'immagine?

### Dockerfile

Il modo raccomandato per farlo è di scrivere un file con le istruzioni. Il file solitamente si chiama Dockerfile
ed ha un suo specifico set di istruzioni. Prendiamo ad esempio il Dockerfile generato per noi da Yeoman seguendo questo [tutorial](/docker-get-started/sessione2).

```
FROM golang
COPY . /go/src/github.com/docker-get-started
RUN go install github.com/docker-get-started
ENTRYPOINT /go/bin/docker-get-started
```

| **Istruzione** | **Descrizione** |
| -------------- | --------------- |
| FROM golang | Specifica l'immagine di base da personalizzare |
| COPY . /go/... | Copia file e directory, presenti nella directory corrente, sul filesystem del container nel path specificato |
| RUN go install ... | Esegue il comando indicato, che compila e installa l'applicazione di esempio |
| ENTRYPOINT cmd | Definisce il comando da eseguire quando verrà avviato il container |

### Build

Una volta definite le istruzioni necessarie per apportare le modiche all'immagine di base e includere i nostri file applicativi, siamo pronti per realizzare la nostra prima immagine.
Da terminale, eseguiamo questo comando:

```
$ docker-compose build
```

Se tutto va bene, dovreste vedere come output qualcosa di questo tipo:  

```
Building helloworld
Step 1 : FROM golang
 ---> 002b233310bb
Step 2 : COPY . /go/src/github.com/docker-get-started
 ---> c49af40580b1
Step 3 : RUN go install github.com/docker-get-started
 ---> 1de51f83b422
Step 4 : ENTRYPOINT /go/bin/docker-get-started
 ---> 8bdb5e4e322a
Successfully built 8bdb5e4e322a
```

### Cosa è successo?

La creazione di un'immagine è un processo incrementale e iterativo, che per ciascuna istruzione presente nel Dockerfile comporta:  
- la creazione di un container basato sull'immagine di base. La prima immagine è quella specificata dal FROM.  
- l'elaborazione dell'istruzione (ad esempio la copia di file, l'esecuzione di un comando, ecc.)  
- il salvataggio del container come nuova immagine che sarà utilizzata dall'istruzione successiva  
- la cancellazione del container
 
Per il Dockerfile di esempio, possiamo notare 4 di queste iterazioni (step), una per istruzione.
L'ultima immagine generata (dallo Step 4) è quella finale che incorpora tutte le nostre personalizzazioni e può essere utilizzata tutte le volte che vorremo. Possiamo verificarne la disponibilità eseguendo da terminale questo comando, cercando l'immagine con ID 8bdb5e4e322a:

```
$ docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
helloworld           latest              8bdb5e4e322a        1 hours ago        671.3 MB
...
```


