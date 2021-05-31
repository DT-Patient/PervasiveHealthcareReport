# Licenza
La licenza con cui sviluppare il nostro sistema software è una scelta molto importante. Prima di selezionarne una in particolare abbiamo effettuato un’attenta analisi su tutte quelle disponibili. 
Per ognuna abbiamo analizzato la loro possibile applicazione all’interno del nostro progetto. 

Le licenze prese in considerazione sono:
- GNU GPLV3
- GNU LGPLV3
- MIT LICENSE
- APACHE LICENSE
- CREATIVE COMMONS

Per ognuna delle precedenti sono stati presi in considerazione pregi e difetti in particolare:

| LICENZA          | PREGI                                                                                                                                                    | DIFETTI                                                            | UTILIZZATA |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|------------|
| GNU GPLV3        | - Free e Open Source<br>- Strong Copyleft                                                                                                                | - No linking                                                       | <br><br>No |
| GNU LGPLV3       | - Sì linking<br>- Free e Open Source<br>- Strong copyleft                                                                                                | - Usata principalmente per le librerie                             | <br><br>No |
| MIT LICENSE      | - Free e Open Source<br>- GPL compatibile                                                                                                                | - Estremamente permissiva<br>- Nessuna protezione per loghi/marchi | <br><br>No |
| APACHE LICENSE   | - Più restrittiva di MIT LICENSE<br>- Specifica delle modifiche effettuate<br>- Utilizzabile se ho dei brevetti<br>- Open può essere linkata, modificata |                                                                    | <br><br>Sì |
| CREATIVE COMMONS | - Buona per rilascio della parte hardware<br>- E' componibile, posso decidere quali diritti rilasciare                                                   | - Non è nata per il software                                       | <br><br>No |

Come si evince dalla tabella, la scelta finale della licenza per il nostro progetto è quindi ricaduta su Apache License 2.0, in quanto risulta essere quella più adatta al software ed inoltre non presenta evidenti difetti. 
La specifica di tale licenza trova applicazione nel file LICENSE, disponibile [*qui*](https://github.com/enrignagna/PervasiveHealthcare/blob/main/LICENSE). 

Seguendo le buone norme di programmazione, ogni file di codice del progetto al suo interno prevede la seguente didascalia per indicare la licenza applicata.

*Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.*


*You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0*


*Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an 
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied.*

*See the License for the specific language governing permissions and limitations under the License."*

[<-- Home](../README.md)