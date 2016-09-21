---
layout: default
---

## Docker Compose

Uno degli strumenti più utilizzati di Docker è il Compose, che consente di definire in un file,
praticamente tutti i comandi e parametri necessari per avviare uno o più container.
Introduce anche il concetto di **servizio** anche se, con l'ultima versione di Docker, questo tema richiede un approfondimento a sè,
che esula dagli obiettivi di questo corso. Come servizio, per ora, limitiamoci a identificare **ogni macro componente** della nostra applicazione,
come ad esempio il processo principale, il database, un processo di test.

### Avviare la nostra applicazione

Tornando alla nostra applicazione di esempio, abbiamo notato come l'esecuzione con Docker tramite il comando Run,
implichi l'utilizzo di numerosi parametri che rendono l'intera istruzione di non facile lettura.  
Docker Compose semplifica la definizione di questi parametri, nascondendo la complessità di avviare un container. 

Proviamo ad utilizzarlo!

### docker-compose.test.yml

Creiamo un nuovo file "docker-compose.test.yml" nella stessa directory del file main.go.  
Editiamo il file aggiungendo queste istruzioni:

```
version: '2'

services:
  helloworld:
    image: golang
    volumes:
      - .:/go/bin/helloworld
    working_dir: /go/bin/helloworld
    command: bash -c "go run main.go"
```
