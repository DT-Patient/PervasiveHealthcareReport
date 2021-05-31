# Scelte implementative salienti
L'implementazione ha rispettato in maniera molto accurata le decisioni prese nella fase di design. Quest'ultima è stata curata notevolmente con lo scopo di avere una visione completa su ogni singolo aspetto che il sistema deve coprire.
L'unica questione che ci preme mettere in risalto, riguarda l'implementazione del pattern CQRS all'interno del sistema. Non essendo disponibile molta documentazione sull'implementazione di questo modello, abbiamo creato una nostra versione che rispetta tutti gli standard teorici definiti dal pattern.


### Comandi e Queries
Ogni comando e ogni query definiti nel sistema sono stati implementati come classi. Queste vengono passate al comand handler per la loro esecuzione. 
Al completamento dell'operazione viene restituito il successo o l'insuccesso di quest'ultima e in caso positivo, vengono memorizzati i dati sul repository.


### Eventi 
Ogni evento è strutturato ed è formato da un ID, un timestamp, un codice dell'evento, per permettere il marshalling/unmarshalling corretto, ed i dati inerenti all'evento stesso.
È stato implementato poi un sistema di utility *RMUtility*, il quale a partire da tutti gli eventi riguardanti uno specifico soggetto,
effettua la creazione dello stesso (i.e. paziente, chirurgo, etc) ricostruendone la versione attuale.

[<-- Home](../README.md)