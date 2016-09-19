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

