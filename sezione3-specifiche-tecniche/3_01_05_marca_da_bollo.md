Marca da Bollo (@e.bollo)
=========================

Tramite la Piattaforma pagoPA è possibile richiedere pagamenti di Posizioni Debitorie che contengano una marca da bollo digitale ("@e.bollo").

Per poter inserire il pagamento di una marca da bollo, è necessario compilare il campo _datiMarcaBolloDigitale_ all'interno dell'RPT avendo cura di inserire:

* _tipoBollo_: tipologia del bollo
* _hashDocumento_: contiene l’impronta informatica (digest), rappresentata in "base 64 binary", del documento informatico o della segnatura di protocollo cui è associata la marca da bollo digitale
* _provinciaResidenza_: sigla automobilistica della provincia di residenza del soggetto pagatore.

Inoltre la RPT non deve contenere, nella struttura `datiSingoloVersamento` relativa alla Marca da Bollo Digitale, la valorizzazione del parametro `ibanAccredito`.

Per maggiori dettagli su @e.bollo, validità e relativi casi d'uso, fare riferimento alla sezione sul sito [dell'Agenzia delle Entrate](https://www.agenziaentrate.gov.it/portale/web/guest/schede/pagamenti/imposta-di-bollo-per-le-istanze-trasmesse-alla-pa-ebollo-cittadini/che-cose-cittadini).