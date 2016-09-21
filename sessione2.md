---
layout: default
---

## Perchè Yeoman?

[Yeoman](http://yeoman.io/){:target="_blank"} è uno strumento opensource che velocizza la creazione di applicazioni.  
Per un corso breve come questo, è utile per generare alcuni file di base che durante la lezione andremo ad analizzare e modificare.
Yeoman è un progetto di successo con tantissimi "generator", come sono chiamati i plugin, per la maggioranza dei linguaggi e dei framework applicativi.  
In particolare useremo lo [Yeoman generator per Docker](https://github.com/Microsoft/generator-docker){:target="_blank"} che è appunto specifico per Docker.

### Yeoman e Docker

Quali file ci serve generare per un progetto Docker?  
Abbiamo visto nella prima lezione l'utilizzo del Docker Compose.
Utilizziamo Yeoman generator per creare il relativo file di configurazione e altri file che discuteremo tra poco.

### Installiamo il Docker generator

Utilizziamo lo strumento [npm](https://www.npmjs.com/) per installare il Docker generator. Da terminale eseguiamo il comando:

```$ npm install -g generator-docker```

Sempre da terminale, spostiamoci nella directory dove è presente il file [main.go](https://github.com/LOG-ED/docker-get-started/blob/master/main.go){:target="_blank"} ed eseguiamo questo comando:

```$ yo docker```

Yeoman mostra una serie di domande a cui dobbiamo rispondere per personalizzare la generazione dei file di configurazione di Docker Compose, a partire dal tipo di linguaggio della nostra applicazione:

![Yeoman Docker generator](/docker-get-started/images/yo-docker.png "Yeoman Docker generator")

Procedete rispondendo alle domande in questo modo:

```
? What language is your project using? Golang
? Does your project use a web server? No
? What do you want to name your image? helloworld
? What do you want to name your service? helloworld
? What do you want to name your compose project? helloword
   create Dockerfile.debug
   create Dockerfile
   create docker-compose.debug.yml
   create docker-compose.yml
   ...
```

### Cosa è successo?

Yeoman ha generato alcuni file per noi tra cui, riconosciamo dal nome, due file di configurazione per Docker Compose.   
Se provate ad editare il file docker-compose.yml o il docker-compose.stage.yml, sono molto simili, vedrete alcune istruzioni di configurazione, molte delle quali non erano state ancora presentate. Vediamole quindi in dettaglio:

```
version: '2'

services:
  helloworld:
    image: helloworld
    build:
      context: .
      dockerfile: Dockerfile
```

| **Istruzione** | **Descrizione** |
| -------------- | --------------- |
| image: helloworld | Indica il nome dell'immagine usata per creare il container |
| build: | Indica che l'immagine non sarà scaricata da un archivio remoto ma deve essere creata adhoc localmente |
| ... context: . | Precisa dove si trova il file con le istruzioni per la creazione dell'immagine |
| ... dockerfile: Dockerfile | Precisa che il file con le istruzioni si chiama Dockerfile |

Se proviamo ad eseguire il Docker Compose con questo file di configurazione, scopriremo che il risultato finale sarà molto simile a quanto avevamo ottenuto durante la [prima sessione del corso](sessione1_1). Eseguendo nel terminale il comando:

```$ docker-compose up```

verifichiamo di ottenere un risultato di questo tipo:

```
...
Creating dockergetstartedfminzoni_helloworld_1
Attaching to dockergetstartedfminzoni_helloworld_1
helloworld_1  | Hello World
dockergetstartedfminzoni_helloworld_1 exited with code 0
```

## Tutto chiaro? Approfondiamo il processo di creazione di un'immagine
