### Comunicazione Dati
Per parlare di processo comunicativo, si parla di 
-  sorgente di informazione
- cammino fisico
- destinatario
L'informazione è l'insieme di dati correlati tra loro. Un esempio è la piramide DIKW.
Il protocollo è l'insieme di regole che consentono la comunicazione e definisce COSA e COME.
Questi Protocolli sono definiti da standard stabiliti da organizzazioni come ISO, IEEE, ICANN, W3C e senza questi definiti due dispositivi non possono comunicare.
Il modello TCP/IP ISO ha 4 layer:
- Network Access
- Internet
- Transport
- Application

### Informazione e misura
L'informazione ha come misura il bit e vale: Q=log<sub>2</sub>M con M numero di stati possibili di un sistema e Q i bit necessari per distinguerli.
Un sistema elaborativo deve avere dei codici per associare le sequenze di bit ad un carattere come BCS, AIKEN, ASCII, UNICODE, ...
I più usati sono l'ascii a  7/8 bit, l'EBCDIC a 8 bit, l'UNICODE.

### Flussi trasmissivi
- Simplex -> unidirezionale
- Half duplex -> bidirezionale a turni
- Full duplex -> bidirezionale diretto

### DTE, DCE, CPE
L'applicazione utente risiede nel Data Terminale Equipment (DTE) come ad esempio un PC.
Il Data Circuit Terminating Equipment (DCE), converte i segnali nella forma migliore per l'invio sul canale.
Il CPE, Custom Premises Equipment si usa in caso sia richiesto un dispositivo di pertinenza dell'utente.

### Le reti ed il loro mondo
La rete è un insieme di dispositivi connessi. Vi sono uno o più nodi capaci di inviare o ricevere dati.
Reti ad elaborazione:
- concentrata -> un DTE potente viene messo a disposizione di altri DTE che ne sfruttano la capacità di calcolo
- distribuita -> DTE diviso in più punti
Per entrambi i modelli vi sono 3 procedure di colloquio:
- Inquiry -> forma di interrogazione messa a disposizione da servizi del PC
- Conversazionale -> stabilisce delle regole e formati, bloccando quelli diversi
- Interattivo -> risponde ad applicazioni sensibili. Invia tutte le applicazione che consentono pieno sfruttamento delle risorse elaborative

### Valutazione della Rete
- Affidabilità -> priva di errori, rimedia ai guasti, gestisce bene le situazioni critiche
- Sicurezza -> protezione dei dati da accesso, perdite e modifiche indesiderate
- Prestazioni ->
	- Ritardo -> misurazione tempo di transito dei dati
	- Tempo risposta -> tempo tra richiesta e risposta
	- Throughput -> quantità di dati spediti in unità di tempo
	Queste dipendono da numero di DTE, tipologia dei mezzi e dal software.
	- Banda -> banda passante di frequenze che può essere usata per la trasmissione dei dati. Massima velocità alla quale è possibile trasmettere informazioni.  Per valutare la velocità di banda si usano strumenti come ping, traceroute, speedtest, pingtest e netindex

### Tipo di trasmissione
- Point-to-Point -> tra due DTE diretti
- Multi-point -> Collegamento condiviso tra più DTE.

### Classificazione delle reti
- WAN -> grandi senza limitazione, DTE distanti, arriva fino a Tbits 
- LAN -> 1 o 2 km, uso privato, arriva fino  a Gbits
- WLAN -> Reti locali Lan ma senza fili. Usa lo spettro radio. La velocità dipende dallo standard usato.
	- 2.4ghz -> offre una copertura ampia ma poco potente
	- 5ghz -> copertura meno ampia ma più potente
- MAN ->livello cittadino, fibra ottica ad alta velocità

### Reti wireless
Usate principalmente per la comunicazione mobile. Abbiamo
- WLAN (802.11)
- WiMax (IEEE 802.16x)
- IEEE 802.20
- CDPD

### Struttura delle reti
La topologia  di una rete è la configurazione geometrica dei collegamenti fra i vari componenti. Sono volte a creare stabilità, a migliorare il rendimento e a diminuire i costi.
- Rete ad albero -> stazioni a livelli, con un livello centrale. Semplice ma vulnerabile
- Rete a dorsale -> collegamento multi punto via ethernet. Questa crea una specie di spina dorsale lungo tutta la rete
- Rete a stella -> ogni nodo è connesso ad un dispositivo centrale. E' più economica rispetto ad una struttura a maglia completa
- Rete ad anello -> molto usata in passato. Ogni nodo ha un punto-a-punto con solo 2 nodi. Ha una trasmissione unidirezionale, ogni nodo rigenera il segnale
- Rete a maglia (MESH) ->tutti i nodi sono collegati tra loro. Il costo totale del percorso è $N(N-1)/2$. Ogni apparato è ha un collegamento Duplex.

### Reti Mesh
Combinazione di nodi fissi e mobili interconnessi tra loro con link wireless per avere una rete autoconfigurante multi-hop.
Offre una grande affidabilità, ha una gestione dinamica dei malfunzionamenti.
Vengono monitorati in tempo reale i percorsi disponibili e selezionati quelli migliori
