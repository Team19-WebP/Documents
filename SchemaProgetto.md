# Appunti per schema

**************************************************************
## Parte pubblica
**************************************************************

--------------------------------------------------------------
### home page 
--------------------------------------------------------------

#### View (home.jsp)
- logo
- immagine rappresentativa
- un testo descrittivo
- pulsante che fa scaricare volantino A5 con info associazione

#### Controller (HomeController.java)
- funzione che permette di recuperare dal database il volantino (forse)

#### Model  ☠️

--------------------------------------------------------------
### Chi siamo
--------------------------------------------------------------

#### View (chiSiamo.jsp)
- descrizione più dettagliata:
	- fondata nel
	- da chi
	- storia
	- sedi
	- riconoscimenti
	- etc
- immagini

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Attività
--------------------------------------------------------------

#### View (attività.jsp)
- breve descrizione delle 3 attività con rispettive immagini
- link alle singole attività

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Pagina attività
--------------------------------------------------------------

#### View (nomeAttività.jsp)
- descrizione dell'attività

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Contatti
--------------------------------------------------------------

#### View (contatti.jsp)
- indirizzo e numero di telefono
- form per inserimento dati dell'utente:
	- nome e cognome
	- email
	- combo box per inserire motivi di contatto con possibilità di 
mettere altro
	- casella di testo multilinea per esplicitare dettagli della 
richiesta
	- tasto per il submit
	- tasto per resettare i campi
- decidere se usare un alert oppure fare un'altra pagina statica per 
_invio confermato_ (vedi sotto)

#### Javascript validation (contatti.js)

#### Controller (MessaggioUtente.java)
Servlet per passare i messaggi al database e che manda una forwarda alla 
pagina _invioConfermato.jsp_ sempre che la facciamo

#### Model (messaggioUtenteBean.java)
Bean che contiene i dati dell'utente.

--------------------------------------------------------------
### Invio confermato
--------------------------------------------------------------
Capire se serve fare una pagina oppure mettere un'alert sulla pagina 
precedente

#### View (invioConfermato.jsp)
- avviso all'utente in cui si conferma la ricezione del messaggio e lo si 
informa che riceverà al più presto una risposta

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Sign-in (io avrei detto o sign-up oppure registrazione)
--------------------------------------------------------------

#### View (sign-in.jsp)
- form con tutti i campi obbligatori
	- nome 
	- cognome
	- data di nascita in formato GG/MM/AAAA (utente deve essere 
maggiorenne)
	- email
	- numero di telefono
	- tipo di utente:
		- simpatizzante 
		- aderente
	- username
	- password da inserire due volte per conferma con i seguenti 
restraint:
		- 8 caratteri
		- deve contenere la prima lettera dei nomi proprio di 
ciascuno di voi (what does it mean??)
		- un carattere maiuscolo
		- un carattere tra i seguenti (! $ ?)
	- un tasto per inviare
	- un tasto per resettare

#### Javascript validation (sign-in.js)
- tutti i campi sono obbligatori
- controllo mail
- controllo password (secondo i criteri)
- controllo che le password siano uguali
- evidenziare di rosso i campi mancanti
- messaggio di errore con relativa informazione dell'errore

#### Controller (Sign-upController.java)
Servlet che prende i dati dell'utente:
- esegue il controllo con il database che l'utente non sia già presente, 
se già presente si effettua una forward con un messaggio di errore 
informativo che inizia con l'id del nostro gruppo
- se l'utente non è presente si registra il nuovo utente nel database e si 
esegue un forward alla pagina di conferma.

#### Model (UserDataBean.java)
Classe java che memorizza i dati dell'utente

--------------------------------------------------------------
### Registrazione confermata
--------------------------------------------------------------

#### View (registrazioneConfermata.jsp)
Messaggio di conferma del nuovo utente

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Login
--------------------------------------------------------------

#### View (login.jsp)
- form che richiede:
	- username
	- password

#### login validation (login.js)
- controllo che i campi non siano vuoti

#### Controller (LoginController.java)
Servlet che controlla i dati inseriti contro il database:
- in caso di errore si effettua il forward alla pagina di login con un 
messaggio di errore informativo che inizia con l'id del gruppo seguito da 
":" e il messaggio di errore
- in caso che vada tutto bene si esegue una forward alla pagina personale 
dell'utente:
	- simpatizzante
	- aderente
	- admin
- l'admin è preregistrato:
	- user: "admin"
	- pass: "19Adm1n!"

#### Model (UserDataBean.java)
Stessa bean di prima dell'utente.

**************************************************************
## Parti comuni
**************************************************************
Il titolo del tab sul browser in cui viene visualizzata la pagina web è il 
nome dell'associazione, che sarà corredato con il logo.

--------------------------------------------------------------
### Intestazione
--------------------------------------------------------------
#### View (intestazione.html)
- nome associazione

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Pie di Pagina
--------------------------------------------------------------
#### View (footer.html)
- nome associazione
- via
- codice postale 5 cifre nel nostro caso 19000
- città
- nazione

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Menu
--------------------------------------------------------------
#### View (menu.html)
- home page (home.jsp)
- chi siamo (chiSiamo.jsp)
- attività (attività.jsp)
- contatti (contatti.jsp)
- sign-up (sign-up.jsp)
- login (login.jsp) che immagino verrà cambiato con un logout

#### Controller ☠️
#### Model ☠️

--------------------------------------------------------------
### Frasi ispiranti
--------------------------------------------------------------
Sezione presente in tutte le pagine con una frase caricata attraverso un 
bean credo che cambia ogni 20 secondi, la frase deve cambiare senza dover 
ricaricare l'intera pagina. 

#### View (frasiIspiranti.jsp)
- frase ispirante caricata con un bean

#### Controller (frasiController.java)
- Servlet chiamata ogni venti secondi che comunica con il database per 
cambiare la frase ispirante

#### Model (frasiBean.java)
- bean con la frase ispirante

**************************************************************
## Parte Privata
**************************************************************

--------------------------------------------------------------
### Simpatizzante
--------------------------------------------------------------
#### View (simpatizzante.jsp)
Dashboard con le operazioni possibili per tale utente (simpatizzante):
- bottone per visualizzare i dati personali (inseriti al sign-in) #🤨 
__vanno inserite anche le attività in cui si sono iscritti??__
- bottone per l'iscrizione ad un'attività (tramite click sull'attività 
oppure con checkbox) 
- bottone per la cancellazione dell'iscrizione del sito

#### Controller 
##### IscrizioniController.java
Servlet per la gestione dell'iscrizione degli utenti alle varie attività 
(se serve)
##### CancellazioneUtente.java
Servlet per la cancellazione dell'utente dal database

#### Model
##### iscrizioniBean.java
Probabilmente un semplice Bean che associa ad un'attività i nomi degli 
utenti iscritti?

--------------------------------------------------------------
### Aderente
--------------------------------------------------------------
#### View (aderente.jsp)
Uguale a simpatizzante.jsp, aggiungendo un include:
- con un campo di testo in cui inserire l'importo (numero intero) e
- bottone per l'invio dell'importo

#### validazione importo con js

#### Controller 
come per i simpatizzanti
##### donazioni.java
Servlet che registra le donazioni

#### Model 
Semplice bean che associa ad un utente una determinata donazione #🤨 __forse non serve da rivedere__

--------------------------------------------------------------
### Amministratore
--------------------------------------------------------------
#### View 
##### (amministratore.jsp)
Pagina dashboard con le operazioni possibili per un amministratore:
- pulsante che mostra tutti gli utenti registrati (utentiRegistrati.jsp)
- pulsante che mostra tutti i simpatizzanti (utentiSimpatizzanti.jsp)
- pulsante che mostra tutti gli aderenti (utentiAderenti.jsp)
- pulsante che mostra il numero di visite che il sito ha ricevuto e 
l'istogramma delle visite per ogni pagina (con possibilità di resettare i 
contatori) (visite.jsp)
- pulsante che mostra le donazioni ricevute mese per mese da gennaio a 
dicembre dell'anno in corso (valore uguale a zero ovviamente se la data è 
futura) (donazioni.jsp)

#### validazione importo con js

##### datiUtenti.jsp
- pagina che mostra una lista di utenti che cambia a seconda del pulsante 
premuto (registrati, simpatizzanti o aderenti)

##### visite.jsp
- pagina che mostra:
	- il numero totale di visite 
	- il numero di visite per ogni pagina
	- un tasto di reset

##### donazioni.jsp
- pagina che mostra un grafico con le donazioni da gennaio a dicembre 
dell'anno in corso ( #🤨 __capire bene la frase: per i mesi dal mese 
successivo a quello della data odierna a dicembre il valore della 
donazione sarà zero????__)
- si riceve un file json dal server che poi tramite highcharts (js) 
verranno visualizzati i grafici

#### Controller 
##### DatiUtentiController.java
servlet per il recupero dei dati degli utenti, si potrebbe impostare un 
parametro nella request "tipo" nel seguente modo:
- registrati: recupera l'elenco di tutti gli utenti ( #🤨 __bisogna capire 
che dati si vogliono recuperare per ogni utente__) e fa il forward a 
datiUtenti.jsp
- simpatizzanti: recupera l'elenco di tutti i simpatizzanti e fa il 
forward a datiUtenti.jsp
- aderenti: recupera l'elenco di tutti gli aderenti e fa il forward a 
datiUtenti.jsp

##### VisiteController.java
Servlet che recupera il valore di tutti i counter, da capire se il numero 
totale delle visite è riferito solamente alla homepage oppure alla somma 
di tutte le pagine.
Con questa servlet è possibile resettare anche tutti i counter.

##### DonazioniController.java
Servlet che richiede al database i dati da mettere in un file json da 
forwardare alla pagina _donazioni.jsp_ per la visualizzazione 
dell'istogramma


#### Model
##### DonazioniBean.java
oggetto creato per essere convertito in un json dalla servlet 
_donazioni.java_
##### CounterBean.java
oggetto per tenere conto le visite per ogni pagina.

