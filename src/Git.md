# Controllo di versione Git
L'implementazione del progetto, oltre agli strumenti di build automation e continuous integration già illustrati precedentemente, ha richiesto l'utilizzo di Git.
Durante il processo di sviluppo abbiamo utilizzato un gran numero di funzionalità che questo strumento mette a disposizione, per permettere di lavorare in cooperazione con tutti gli elementi del team di sviluppo.

## Git Flow
Git Flow è un flusso di lavoro Git che ci ha aiutato nello sviluppo del software e nell'implementazione delle pratiche DevOps. Il flusso di lavoro di Gitflow definisce un modello di ramificazione rigoroso progettato attorno alla versione del progetto, fornendo una solida struttura per la gestione di progetti di medie e grandi dimensioni.

Il flusso di lavoro è costituito da due rami principali:
- main, contenente la versione stabile del codice realizzato
- develop, il quale nasce con lo scopo di seguire lo sviluppo e la crescita del codice.

Assieme a questi due rami principali è possibile sfruttare i seguenti rami per svolgere azioni differenti, in base allo stato del sistema.
- feature, per lo sviluppo di feature aggiuntive del sistema
- release, per il rilascio di una release stabile del sistema
- hotfix, per la risoluzione di un bug rilevato nel codice.

## Squashing 
Un’altra funzionalità importante di Git è lo squashing. Si utilizza quando si hanno più commit e si vogliono schiacciare in un unico commit per varie motivazioni.
Lo squashing è una modifica grossa perché non conserva tutti commit, in quanto vengono interamente sovrascritti dal nuovo commit.
Durante lo sviluppo del progetto abbiamo utilizzato varie volte questa tecnica per
pulire la storia del nostro software o raggruppare alcuni commit effettuati durante lo sviluppo dei workflow di CI o dei file per la BA.

## Rebasing
La tecnica di rebasing è stata sfruttata in maniera limitata, ma si sono verificate casistiche in cui è risultato necessario effettuare rebase. 
La casistica principale consiste nell'avanzamento del ramo develop, con dei rami feature aperti. Nel momento in cui la feature risulta completa e la si vuole portare sul ramo di sviluppo principale, questo può aver subito delle modifiche successive al momento in cui era stato aperto il ramo della feature.
Risulta necessario eseguire il rebase di quest'ultimo ramo sul ramo develop, in modo da mergiare la feature senza imbattersi in problematiche.

## Tagging e Release
Dalla prima versione funzionante del progetto sono stati aggiunti dei tag per indicare il versionamento del software. I tag utilizzati sono di tipo *annotated* ma privi di firma.
Per le versioni in cui sono variate major o minor nel numero di versione, è stata rilasciata la release del progetto sulla piattaforma Github, con un piccola descrizione dei principali cambiamenti.

[<-- Home](../README.md)