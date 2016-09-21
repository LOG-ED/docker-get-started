---
layout: default
---

## Docker Compose

Uno degli strumenti più utilizzati di Docker è il Compose, che consente di definire in un file,
praticamente tutti i comandi e parametri necessari per avviare uno o più container.
Introduce anche il concetto di **servizio** anche se, con l'ultima versione di Docker, questo tema richiede un approfondimento a sè,
che esula dagli obiettivi di questo corso. Come servizio, per ora, limitiamoci a identificare **ogni macro componente** della nostra applicazione,
come ad esempio il processo principale, il database, un processo di test.

### Perchè utilizzarlo?

Tornando alla nostra [applicazione di esempio](https://github.com/LOG-ED/docker-get-started/blob/master/main.go){:target="_blank"}, abbiamo notato come l'esecuzione con Docker tramite il comando Run,
implichi l'utilizzo di numerosi parametri che rendono l'intera istruzione di non facile lettura.  
Docker Compose semplifica la definizione di questi parametri, nascondendo la complessità di avviare un container. 

### Proviamo ad utilizzarlo!

Creiamo un nuovo file **"docker-compose.test.yml"** nella stessa directory del file main.go.  
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
In queste istruzioni, possiamo riconoscere alcuni comandi e parametri:

| **Istruzione** | **Descrizione** |
| ---------- | ----------- |
| image: golang | Indica l'immagine di base da utilizzare |
| volumes: - .:/go/bin/helloworld | Definisce il "mapping" tra la directory corrente dell'host e la directory /go/bin/helloworld del container |
| working_dir: /go/bin/helloworld | Definisce la directory del container dove verrà eseguito il command |
| command: bash -c "go run main.go" | Indica il comando da eseguire nella bash una volta creato il container |

### Avviamo l'applicazione

Docker compose è utilizzato principalmente per avviare i servizi definiti in un file di configurazione, come il **"docker-compose.test.yml"** che abbiamo creato.  
Apriamo un terminale e spostiamoci nella directory dove è presente il file di configurazione. Utilizziamo il seguente comando per avviare il servizio helloworld, ovvero per creare un nuovo container in cui verrà eseguita la nostra applicazione di esempio:

```$ docker-compose -f docker-compose.test.yml up```

Se non otteniamo errori, il risultato atteso è di vedere visualizzato nel terminale qualcosa di simile a:

```
Creating dockergetstarted_helloworld_1
Attaching to dockergetstarted_helloworld_1
helloworld_1  | Hello World
dockergetstarted_helloworld_1 exited with code 0
```

### Cosa è successo?

Docker compose, sulla base del file di configurazione indicato con il parametro -f, ha tentato di creare un nuovo container
per il servizio helloworld con questa naming convention: **progetto_servizio_counter**. Ad esempio, nel nostro caso, se il nome del container corrisponde a **dockergetstarted_helloworld_1** è perchè:  
- la directory corrente è docker-get-started  
- il servizio si chiama helloworld  
- stiamo creando il primo container per il servizio  

Creato il container, è stato eseguito il comando che prevedeva la compilazione ed esecuzione della nostra applicazione di esempio. Finita l'esecuzione del comando, il container è stato terminato senza erorri (exited with code 0).
