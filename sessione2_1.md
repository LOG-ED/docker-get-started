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
| ENTRYPOINT /go/bin/... | Definisce il comando da eseguire quando verrà avviato il container |


