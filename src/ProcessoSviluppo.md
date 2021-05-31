# Processo di sviluppo adottato
Il processo di sviluppo adottato segue la metodologia DevOps.
Il nostro team è perciò formato da 3 componenti con incarichi differenti:
- *Battistini*, addetto DevOps e sviluppatore.
- *Gnagnarella*, addetto DevOps e sviluppatore.
- *Scucchia*, sviluppatore e committente del progetto.

Il processo di sviluppo prevede il supporto nell'intero ciclo di vita del progetto dei vari strumenti che la filosofia DevOps mette a disposizione, come build automation e continuous integration.


## GitHub Organization 
Per una corretta organizzazione del progetto e dei sistemi sviluppati per affiancare il suo ciclo di sviluppo,
abbiamo creato l'organizzazione [DT-Patient](https://github.com/orgs/DT-Patient/dashboard).
Quest'ultima al suo interno contiene 4 repository:
- BuildAutomationSetup
- Pervasive Healthcare
- Pervasive Healthcare Report
- UpGradle Bot

La creazione di una organizzazione è stata effettuata in un secondo momento. In un primo momento tutti i repository erano realizzati attraverso l'account di un solo membro del
gruppo e condivisi con gli altri collaboratori. A seguito dello sviluppo della documentazione
e del bot per l'aggiornamento delle dipendenze, ci siamo resi conto che questa soluzione avrebbe permesso un funzionamento migliore,
in quanto consente un settings più semplice per il bot e un raggruppamento migliore per i vari repository creati per il progetto.

### Repository sviluppati
#### BuildAutomationSetup
Questo repository contiene al suo interno un progetto Gradle con le impostazioni iniziali per quanto riguarda la BA di un sistema.
Nasce con lo scopo di essere un template per la realizzazione di altri sistemi software.
Lo sviluppo del nostro elaborato *Pervasive Healthcare* e della sua documentazione *PervasiveHealthcare Report* sono partiti proprio da questo template.
Il repository *buildautomationsetup* è disponibile [qui](https://github.com/DT-Patient/buildautomationsetup).

#### Pervasive healthcare
Progetto principale, sviluppato per il corso di Pervasive Computing e LSS. Questo repository contiene il nostro sistema 
software, che comprende anche il codice sviluppato per la build automation e i workflow di GitHub Actions.
Il software presente all'interno di questo sistema è stato progettato seguendo la metodologia Domain Driven Design.
La documentazione *ScalaDoc* del progetto è stata pubblicata sul [dominio](https://dt-patient.github.io/PervasiveHealthcare/) Github Pages di questo repository.

#### Pervasive healthcare Report
La documentazione realizzata per il corso di LSS, ovvero il report del progetto è stato sviluppato in markdown e mantenuto in questo repository.
Questa suddivisione col progetto vero e proprio è stata fatta per avere una separazione dei concetti. In aggiunta avendo due repository differenti,
abbiamo sfruttato il [dominio](https://dt-patient.github.io/PervasiveHealthcareReport/) offerto da questo repository per pubblicare la relazione di progetto, sfruttando il framework Jekyll
per convertire i file markdown in un sito web.

#### UpGradle Bot
Bot realizzato sfruttando il sistema [UpGradle](https://github.com/DanySK/upgradle), sviluppato dal professor Danilo Pianini.
Attraverso la realizzazione del bot dentro l'organizzazione DT-Patient, ogni progetto mantiene aggiornate le proprie dipendenze.
Il funzionamento del bot prevede la sua esecuzione, ogni giorno alle ore 02:00, per controllare tutte le dipendenze dei progetti specificati.
Nel caso in cui vengano rilevati degli aggiornamenti, effettua una pull request sul ramo develop per aggiornare il file *versions.properties* con l'ultima versione della dipendenza.


## Tool di DevOps
In questa sezione sarà introdotto il processo di BA e CI, che ha accompagnato e automatizzato molteplici operazioni durante l'intero sviluppo del software.

### Build Automation
La build automation ha permesso di automatizzare un'ampia varietà di compiti nelle nostre attività quotidiane di sviluppo come:
- compilazione del codice sorgente in codice binario
- pacchettizzazione del codice binario
- esecuzione di test
- creazione di documentazione

#### Struttura del progetto
L'intero sistema è stato progettato con una struttura gerarchica a sotto progetti.
All'interno è stato definito un file build.gradle.kts comune a tutte le sottoparti, che appunto definisce dipendenze, plugin e funzionalità comuni.
Ogni specifico sotto progetto, estende il file di build comune ed ad esso va ad aggiungere le specifiche funzionalità a lui necessarie. Tutto questo è possibile includendo le configurazione comuni all'interno dei singoli sotto progetti ed estendendole.


#### Plugin
Il nostro progetto è sviluppato principalmente in linguaggio Scala, quindi sono stati importati i plugin specifici per tale linguaggio. Abbiamo utilizzato, in aggiunta, 
il plugin *Jacoco*, per il controllo della coverage all'interno del progetto ed il plugin di [Semantic Versioning](https://github.com/DanySK/git-sensitive-semantic-versioning-gradle-plugin), 
realizzato dal professor Danilo Pianini, per riuscire a controllare la corretta versione del software.
Per garantire il corretto funzionamento di questi ultimi sono state definiti dei settings appositi sall'interno del file *build.gradle.kts*.

#### Dipendenze
Il sistema Pervasive Healthcare essendo un ambiente di dimensioni moderate ha visto l'utilizzo di un gran numero di librerie esterne, le quali sono state importate in maniera opportuna, in base al loro utilizzo nell'implementazione od esclusivamente nei test. In aggiunta nei repository di riferimento sono state inserite le piattaforme in cui andare a reperirle per includerle nel progetto.

#### Refresh automatico delle dipendenze
All'interno del file *settings.gradle.kts*, è stato abilitato il refresh automatico delle versioni delle dipendenze. Questo sistema permette appunto di andare ad aggiornare tutte le dipendenze e librerie presenti nel progetto, in modo da disporre sempre della versione aggiornata.
Questa funzionalità a fianco di un sistema di build e testing automatizzato permette di verificare costantemente se le nuove versioni delle dipendenze compromettono il nostro software.



### Continuous Integration
La CI, a seguito dell'implementazione della BA, è un punto centrale nella filosofia DevOps. All'interno del progetto è stata sviluppata sfruttando la piattaforma Github Actions, che permette di definire delle pipeline per l'esecuzione di build, test e deployment in ambienti differenti.
Nel nostro sistema sono stati definiti 5 workflow, rispettivamente per la build del progetto, per la build delle pull request esterne, per la pubblicazione della documentazione sul dominio offerto da Github, per la creazione del ramo di release ed infine per la pubblicazione delle release. Di seguito verranno spiegati più nel dettaglio i vari workflow.

#### Build workflow
Questo workflow reagisce all'evento di push rispettivamente sui branch **main** e **develop**; in aggiunta a ciò, è stato impostata l'esecuzione periodica ogni lunedì alle ore 02:00.
L'esecuzione di questo workflow viene svolta sulla combinazione di sistemi:
- Sistema operativo:
  -  Windows
  - MacOs
  - Ubuntu
- Versione JVM:
    - 8
    - 11
    - 14
    - 15
    
Gli step eseguiti prevedono una serie di operazioni di preparazione dell'ambiente di esecuzione:
- il controllo del repository
- l'installazione del JDK

Di seguito vengono svolti i seguenti processi, realizzati come script bash: build e check del progetto.
Quest'ultimo permette la creazione del coverage report tramite Jacoco ed il linting del progetto tramite Spotless.
Successivamente il report di Jacoco viene inviato alla piattaforma Codecov, tramite l'apposita action *codecov-action@v1*.


#### Build pull request workflow
Questo workflow reagisce all'evento di una pull request esterna al repository.
L'esecuzione di questo workflow viene svolta sulla combinazione di sistemi:
- Sistema operativo:
  -  Windows
  - MacOs
  - Ubuntu
- Versione JVM:
  - 8
  - 11
  - 14
  - 15

Per quanto riguarda gli step eseguiti sono previste una serie di operazioni iniziali per la preparazione dell'ambiente di esecuzione, le quali rispecchiano quelle eseguite nel workflow precedente.

Di seguito vengono svolti i seguenti processi, realizzati come script bash: build e check del progetto.
Quest'ultimo permette la creazione del coverage report tramite Jacoco ed il linting del progetto tramite Spotless.
Successivamente il report di Jacoco viene inviato alla piattaforma Codecov, tramite l'apposita action *codecov-action@v1*.

#### Website workflow
Questo workflow reagisce all'evento di una release.
A seguito dell'avvio del workflow viene eseguito un controllo del repository, viene generata la documentazione del progetto la quale ,infine, viene caricata sul branch *gh-pages*.
La documentazione è visibile tramite il dominio offerto da Github.

#### Create release branch workflow
Questo workflow non reagisce a nessun evento, infatti viene avviato manualmente dallo sviluppatore quando si vuole creare un ramo di release.
All'avvio vengono richiesti i seguenti dati in input:
- numero di versione
- note di rilascio *(facoltative)*

Successivamente il workflow al suo interno svolge i seguenti step:
- checkout del repository
- creazione del ramo release con il nome della versione scelto
- aggiornamento della versione e delle note nel file *app_versions.gradle*
- commit del file *app_versions.gradle*
- push del nuovo branch release su origin  
- creazione di una pull request sul ramo main 
- creazione di una pull request sul ramo develop

La creazione delle pull request viene effettuata tramite l'action *thomaseizinger/create-pull-request@1.0.0*.
L'accettazione delle pull request è poi demandata allo sviluppatore, per consentire un ultimo controllo prima della creazione della release vera e propria.



  

#### Tagging relase workflow
A seguito del merging della pull request, creata dal workflow *Create Release Branch*, viene avviato automaticamente questo workflow.
Il suo scopo è quello di creare la release e pubblicarla su GitHub nell'apposita sezione.
Questo workflow al suo interno vede il susseguirsi dei seguenti step:
- checkout del repository
- recupero del numero di versione dal file *app_versions.gradle*
- recupero delle note di rilascio dal file *app_versions.gradle*

Terminati tutti gli step viene creata la release attraverso *actions/create-release@v1*.
  


### Pubblicazione su Maven
Dopo una lunga riflessione fra i membri del team, abbiamo deciso all'unanimità di non effettuare nessuna pubblicazione su Maven Central. 
Le motivazioni che ci hanno portato a non pubblicare sono caratterizzate principalmente dal software dai noi realizzato.
Essendo il sistema una versione prototipale e non contenendo nessuna libreria rilevante da noi realizzata, abbiamo perseguito questa strada,
pur avendo già richiesto un group ID e avendo testato i passaggi per effettuare una pubblicazione su altri repository di studio realizzati precedentemente.

[<-- Home](../README.md)