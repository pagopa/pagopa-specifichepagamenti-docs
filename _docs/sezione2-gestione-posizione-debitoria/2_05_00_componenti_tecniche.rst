Componenti tecniche del Nodo
============================

Il Nodo definisce modalità standard per la gestione dei flussi
finanziari:

-  adotta gli standard `XML ISO
   20022 <https://en.wikipedia.org/wiki/ISO_20022>`__ per i tracciati
   dei flussi finanziari correlati alle singole operazioni;
-  introduce uno standard per la richiesta di pagamento telematico e per
   la ricevuta telematica di pagamento adottato a livello nazionale su
   qualunque canale di pagamento, al fine di automatizzare la tratta G2B
   (*Government to Bank*);
-  nell’ambito delle attività legate al commercio elettronico abilita
   l’interconnessione con i circuiti internazionali di autorizzazione di
   tali pagamenti;
-  assicura l’univocità del pagamento attraverso la definizione di un
   codice identificativo del pagamento (IUV). Al suddetto identificativo
   può essere associato uno o più oggetti grafici (codice a barre,
   glifo, QR-code, etc), al fine di consentire e facilitare
   l’effettuazione del pagamento attraverso qualunque canale oggi
   esistente;
-  de-materializza tutte le ricevute di pagamento restituite all’EC;
-  de-materializza gli avvisi di pagamento.

Nella figura che segue sono evidenziate le componenti ed i soggetti che
interagiscono tra di loro per consentire lo svolgersi del processo di
pagamento telematico secondo i modelli descritti in precedenza:

.. figure:: ../images/bbd_architettura.png
   :alt: architettura-pagoPA

   architettura-pagoPA

Si noti che sebbene le funzionalità di alto livello ed i relativi flussi
di informazione siano ben definiti, le sottostanti implementazioni e le
architetture interne possono evolvere nel tempo (es: le PdD sono state
deprecate nel 2017 ma attualmente ancora utilizzate).

Gestore del Workflow Applicativo
--------------------------------

È la macro-componente principale che ha lo scopo di coordinare
l’esecuzione delle richieste di servizio, richiamando componenti di
utilità (quali ad esempio, il modulo per la diagnostica) ed
interfacciare l’infrastruttura di Rete SPC.È la macro-componente
principale che ha lo scopo di coordinare l’esecuzione delle richieste di
servizio, richiamando componenti di utilità quali ad esempio, il modulo
per la diagnostica, e di interfacciare l’infrastruttura di Rete.

Il *Gestore del Workflow Applicativo* interfaccia sia le applicazioni
degli EC da cui provengono le richieste di servizio e a cui devono
essere indirizzate le relative risposte applicative, sia i PSP che
abilitano il pagamento sui diversi canali.

Comprende vari agenti software tra cui i principali sono quelli che
permettono:

-  la gestione del “Giornale degli Eventi” dove sono registrati - per
   ogni operazione - tutti gli scambi necessari alla corretta esecuzione
   del processo;
-  la gestione del “Tavolo Operativo” dove sono monitorati tutti i
   componenti del sistema e lo stato di esecuzione delle operazioni;
-  l’indirizzamento ai singoli servizi e/o sotto-servizi in funzione
   delle richieste e delle risposte previste dai diversi modelli di
   funzionamento;
-  la memorizzazione e la gestione delle “richieste di servizio” per la
   tracciatura delle operazioni e la gestione delle eccezioni;
-  la gestione degli errori;
-  il mantenimento del sincronismo temporale.

Gestore della Connessione
-------------------------

La connessione al Nodo in applicazione al vigente modello di
interoperabilità avviene nelle forme e nei metodi descritti nel
documento collegato `“Specifiche di Connessione al sistema
pagoPA” <https://github.com/pagopa/lg-pagopa-docs/blob/master/documentazione_tecnica_collegata/documentazione_collegata/Sistema_pagoPA_-_Specifiche%20connessione_2.3.pdf>`__,
disponibile sul sito istituzionale di PagoPA S.p.A.

Gestore della Porta di Dominio
------------------------------

|work-in-progress| **Paragrafo soggetto a proposta di modifica**

Questa componente, deprecata e mantenuta per retro compatibilità, si
occupa dello scambio dei messaggi da e verso SPC per il colloquio con
l’EC secondo gli accordi di servizio stabiliti dalle regole tecniche
SPCoop e pubblicati sui registri SICA. In coerenza con le logiche
SPCoop, permette di reindirizzare i messaggi alle Pubbliche
Amministrazioni aderenti a SPC anche in via indiretta attraverso le reti
territoriali, eventualmente per mezzo di soggetti intermediari.

Tra le principali attività svolte dalla componente si richiamano, a
titolo esemplificativo:

-  incapsulamento delle chiamate dei metodi *Web service*, rendendole
   disponibili in forma mediata verso la Porta di Dominio;
-  memorizzazione temporanea e trattamento, secondo la priorità
   indicata, dei messaggi verso la Porta di Dominio;
-  tracciamento dei riferimenti univoci dei messaggi;
-  trattamento degli header dei messaggi scambiati via Porta di Dominio
   ai fini della correlazione applicativa attuata dalla Porta di Dominio
   stessa;
-  gestione degli errori e delle conferme di natura trasmissiva;
-  generazione e propagazione dei messaggi d’errore di natura
   applicativa;
-  mantenimento di un proprio registro degli eventi finalizzato
   all’aggiornamento del Giornale degli Eventi;
-  mantenimento del sincronismo temporale.

Interfaccia di Canale
---------------------

Le attività svolte da questa componente sono analoghe a quelle svolte
dal gestore della Porta di Dominio per gli Enti Creditori, ma istanziate
per il rapporto con i singoli PSP. A tale scopo, il Nodo espone una
modalità standard di colloquio verso i PSP, descritta nella Sez-IV. Nel
caso di peculiari modalità tecnico trasmissive richieste dai PSP, sempre
che di validità generale, possono essere realizzate allo scopo
specifiche interfacce software.

Qualora il PSP lo richieda, la componente permette di interfacciare il
PSP attraverso un intermediario (soggetto giuridico o circuito) scelto
dallo stesso PSP. Tutti gli oneri derivanti sono a carico del PSP che
mantiene la titolarità del rapporto con il Nodo.

Di seguito le principali attività svolte dalla componente:

-  incapsulamento delle chiamate al fine di renderle disponibili in
   forma mediata verso gli specifici canali;
-  memorizzazione temporanea dei messaggi applicativi verso i canali;
-  tracciamento dei riferimenti univoci dei messaggi
   memorizzati/inviati;
-  gestione degli errori e delle conferme di natura trasmissiva;
-  generazione e propagazione dei messaggi d’errore di natura
   applicativa;
-  mantenimento di un proprio registro degli eventi finalizzato
   all’aggiornamento del Giornale degli Eventi;
-  mantenimento del sincronismo temporale.

Repository ricevute telematiche
-------------------------------

Il *Repository* costituisce l’archivio in cui sono memorizzate tutte le
ricevute telematiche processate dal Nodo e non ancora consegnate,
finalizzato al buon funzionamento del sistema. Esso consente una
verifica in merito al corretto trattamento dei flussi di pagamento del
Nodo.

Componente Web-FESP
-------------------

La componente “Web-FESP” permette di effettuare il pagamento
reindirizzando l’Utilizzatore finale verso una *landing page* messa a
disposizione dal PSP.

In questo caso:

-  il PSP consente all’Utilizzatore finale di eseguire il pagamento con
   i diversi strumenti di pagamento;
-  la componente Web-FESP agisce da normalizzatore e provvede ad
   uniformare le informazioni ricevute, re-inviandole, attraverso il
   Nodo, all’EC per consentire di completare l’operazione di pagamento.

Componente WISP
---------------

La componente “WISP” (*Wizard Interattivo di Scelta del Prestatore di
Servizi di Pagamento*) consente all’utilizzatore finale di effettuare la
scelta del PSP in modalità accentrata presso il Nodo, che mette a
disposizione apposite pagine che standardizzano a livello nazionale la
*user experience* dei pagamenti verso la Pubblica Amministrazione,
garantendo ai PSP aderenti che l’esposizione dei servizi da loro offerti
sia proposta all’Utilizzatore finale attraverso schemi che consentano
pari opportunità di trattamento, concorrenza e non discriminazione.

La componente WISP inoltre fornisce all’Utilizzatore finale funzioni di
supporto introducendo vari accorgimenti per semplificare la *user
experience*, anche nel caso di pagamento con dispositivi mobili. Inoltre
l’Utilizzatore finale potrà memorizzare gli strumenti di pagamento
utilizzati, evitando di dover effettuare una nuova ricerca nelle
occasioni successive.

File Transfer sicuro
--------------------

|work-in-progress| **Paragrafo soggetto a proposta di modifica**

Il Nodo mette a disposizione dei soggetti aderenti una piattaforma
*client-server* per il trasferimento sicuro dei dati in modalità *File
Transfer*. Tale piattaforma sostituirà progressivamente l’utilizzo delle
primitive oggi impiegate per lo scambio di informazioni in modalità
massiva (ad esempio: i flussi di rendicontazione, i totali di traffico,
etc).

.. |work-in-progress| image:: ../images/wip.png
