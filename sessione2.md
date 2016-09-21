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

![Yeoman Docker generator](/images/yo-docker.png "Yeoman Docker generator")



