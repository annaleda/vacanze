# Questionario Adeguata Verifica (TCM)

## Ticket Correlati all'Attività

- **Ticket ID**: `BV-164 - JvRomeo - Integrazione servizi Provisio per componente vita TCM (stand alone/CPI miste)`
- **Ticket ID**: `BV-177 - JvRomeo - Api Provisio - Implementazione client generico`
- **Ticket ID**: `BV-178 - JvRomeo - Api Provisio - Implementazione chiamata AddSurvey`
- **Ticket ID**: `BV-179 - JvRomeo - Api Provisio - Implementazione chiamata GetSurvey`
- **Ticket ID**: `BV-250 - JvRomeo - Api Provisio - Implementazione chiamata CheckList`
- **Ticket ID**: `BV-251 - JvRomeo - Api Provisio - Implementazione chiamata CheckRiskProfile`
- **Ticket ID**: `BV-231 - JvRomeo - Api Provisio - Implementazione chiamata GetPdfSurvey`
- **Ticket ID**: `BV-231 - JvRomeo - Api Provisio - Implementazione chiamata ConsolidateSurvey`
  
## Dipendenze / Prerequisiti

- **Prerequisiti**: Censimento a db delle property per acquisire l'url degli swagger dei servizi esterni.

## Descrizione dell'Implementazione Tecnica

* **PASS-PLATFORM**:
  - Client apposito `com/rgigroup/ext/rest/clients/provisio/implclient`
  - Nuovi servizi rest in estensione racchiusi dentro la classe **ProvisioApi** con endopoint disponibili:
  * **POST** `provisio/questionRT/AddSurvey` : inizializzazione di un nuovo questionario da compilare.
  * **GET**  `provisio/questionRT/GetSurvey/{codQuest}` : restituisce lo stato del questionario (C=comploetato) e i dati inerenti ai Beneficiari, la chiamata si occupa anche del salvataggio dei soggetti.
  * **POST** `provisio/kycRT/CheckRiskProfile` : restituisce il codice della valutazione del profilo di rischio e lo stato .
  * **POST** `provisio/kycRT/CheckList/v1` : restituisce un codice di valutazione e un allarme contenete uno stato per ogni soggetto da scansionare.
  * **POST** `provisio/questionRT/ConsolidateSurvey` : serve per inserire dell'info aggiuntiva a posteriori, nel caso dell'emissione serve di mandare il numero proposta e il numero di polizza dopo che è stata emessa la polizza.
  * **GET**  `provisio/questionRT/GetPdfSurvey/{codQuest}` : restituisce il pdf riguardante il questionario di adeguata verifica.
 
* **PASS-PORTAL**: angularjs, inserito un nuovo modulo `provisio` che contiene una direttiva contenente la logica di apertura della modale al questionario di adeguata verifica presente sul FE esterno di corvallis, la direttiva inserita della pagina dei dati tecnici, si occupa di effettuare le relative chiamate ai servizi. Se il questionario non è compilato non si puo procedere alla pagina dei dati di bene.
In base alle risposte dei servizi di check è possibile, per alcune combinazioni delle risposte, mandare in autorizzazione la proposta.
(Formule di PP).


## Moduli Impattati

* **PASS-PLATFORM** : Client, servizi rest, models per tutti i DTO necessari.
* **PASS-PORTAL**   : angularjs, aggiunta de nuovo modulo provisio.

## Configurazioni Necessarie

- **piSystemProperties**: -
- **Java System Properties (-D)**: -
- **Altre Configurazioni**: -

## Configurazioni PP

- Formule per il blocco che manda in autorizzazione la proposta
- Censita proprietà personalizzata Prodotto Vita PRDVIT 

## Componente DB

- **DB Coinvolto**: No
  - **Tabelle Modificate**: -
  - **Query o Procedure Modificate**: -
  - **Tabelle Aggiunte**:
   

## File Impattati

- Elenco dei file modificati, con un breve commento sulle modifiche principali apportate.

## Commit Git

- **Commit ID**: Elencare gli ID dei commit rilevanti e un breve commento per ciascuno.
