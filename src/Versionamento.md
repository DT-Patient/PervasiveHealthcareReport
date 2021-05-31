# Versionamento
Il versionamento permette di associare un identificativo univoco ad una certa versione del software. Git genera di default un hash per ogni commit, in modo da marcare automaticamente ogni cambiamento al software, ma non essendo il valore di hash né progressivo né lineare, abbiamo aggiunto un ulteriore tecnica di versionamento del software al nostro progetto.

La scelta della tecnica di versionamento da utilizzare ha tenuto conto di vari aspetti. 
Oggi giorno ce n'è una in particolare che è ampiamente utilizzata in quanto fornisce un sistema semplice da applicare e con politiche rigide in modo da non creare confusione fra le varie versioni di software rilasciate.
In aggiunta permette a colpo d’occhio di comprendere quanto un software è cambiato rispetto alla versione precedente.
La tecnica scelta per il nostro software è il *Semantic Versioning*.

Questa tecnica di versionamento segue questa politica per l'assegnamento del numero di versione:

#### MAJOR.MINOR.PATCH

dove si incrementa:
- Versione MAJOR, quando apporti modifiche API incompatibili,
- Versione MINOR, quando si aggiungono funzionalità in modo compatibile con le versioni precedenti
- Versione PATCH, quando si apportano correzioni di bug compatibili con le versioni precedenti


Oltretutto persiste una policy di no-retract, ovvero una volta assegnata una versione non si può retrocedere con il numero di versione.
In tal modo si riduce di molto la confusione nella comprensione della versione del codice rilasciato.


[<-- Home](../README.md)