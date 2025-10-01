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
- Conversational -> stabilisce delle regole e formati, bloccando quelli diversi
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
- Point-to-Point -> tra due DTE diretti mediante linea telefonica o dedicata
- Multi-point -> Collegamento condiviso tra più DTE. La condivisione avviene in maniera temporale o condivisone dello spazio del canale.

### Classificazione delle reti
- WAN -> grandi senza limitazione, DTE distanti, arriva fino a Tbits. Sono distribute, quindi anche se un nodo cade, il routing instrada verso un'altra Path.
- LAN -> 1 o 2 km, uso privato, arriva fino a migliaia Gbits. Possono esserci alcuni DTE che fungono da server. 
- WLAN -> Reti locali Lan ma senza fili. Usa lo spettro radio. La velocità dipende dallo standard usato.
    - wifi 5 802.11ac 3.5gbps
    -  wifi 6 802.11ax 9.6 gbps
    - 2.4ghz -> offre una copertura ampia ma poco potente
	- 5ghz -> copertura meno ampia ma più potente
- MAN ->livello cittadino, fibra ottica ad alta velocità
*Docker*
Per sicurezza tutti i software in genere girano come demoni separati all'interno dei software server
### Reti wireless
Usate principalmente per la comunicazione mobile. Abbiamo
- WLAN (802.11)
- WiMax (IEEE 802.16x)
- IEEE 802.20
- CDPD (Cellular Digital Packet Data)

### Struttura delle reti
La topologia  di una rete è la configurazione geometrica dei collegamenti fra i vari componenti. Sono volte a creare stabilità, a migliorare il rendimento e a diminuire i costi.
- Rete ad albero -> stazioni a livelli, con un livello centrale. Semplice ma vulnerabile
- Rete a dorsale -> collegamento multi punto via Ethernet. Questa crea una specie di spina dorsale lungo tutta la rete. Questa rete richiedeva anche una speciale terminazione montata a fine del cavo.
- Rete a stella -> ogni nodo è connesso ad un dispositivo centrale. E' più economica rispetto ad una struttura a maglia completa. Ad esempio un ethernet con tipologia a stella aveva un doppino UTP non schermato, quindi in plastica.
- Rete ad anello -> molto usata in passato. Ogni nodo ha un punto-a-punto con solo 2 nodi. Ha una trasmissione unidirezionale, ogni nodo rigenera il segnale.  Non supporta errori
- Rete a maglia (MESH) -> tutti i nodi sono collegati tra loro. Il costo totale del percorso è $N(N-1)/2$. Ogni apparato è ha un collegamento Duplex.

### Reti Mesh
Combinazione di nodi fissi e mobili interconnessi tra loro con link wireless per avere una rete auto-configurante multi-hop.
Offre una grande affidabilità, ha una gestione dinamica dei malfunzionamenti, sia per quanto riguarda il collegamento radio che per quanto riguarda la componente hardware della rete.
Vengono monitorati in tempo reale i percorsi disponibili e selezionati quelli migliori

Sono soggette ad un alto tasso di errore visto l'utilizzo di onde radio, dunque serve sviluppare protocolli ottimizzati per il wireless.
La maglia usata tra gli accesso point forma il wireless back haul multi hop, un sistema di comunicazione che fornisce ad ogni utente servizi a basso costo multi hop a banda larga.
- Back haul network = rete comprendente nodi intermedi tra dorsale e nodi periferici
La rete Mesh risolve le seguenti esigenze:
- trasmissione in movimento e simmetrica (up-link down-link)
- limiti di banda delle strutture ad albero
- reti ad-hoc senza infrastruttura
- configurazione automatica
- radiolocalizzazione senza GPS
- resistenza alle interferenze
- 100% degli IP utilizzabili
- più sicurezza

### WI-FI vs MESH
Nelle reti wifi un guasto blocca tutta la rete mentre nelle reti mesh si ha maggiore tolleranza ai guasti e flessibilità nella pianificazione.

### I Protocolli secondo ISO-OSI
Il compito dei protocolli, ovvero chi gestisce il colloqui tra due DTE o DCE è:
- gestire il flusso dei dati e gli scambi
- controllo degli errori
- sincronizzazione
- strutturare i dati trasmessi
I protocolli per le relazioni tra due DTE si possono dividere in:
-  Ambito Primario/Secondario:
	-  Polling/selecting
	- BSC
	- HDLC
	- SNRM
	- RST/CTS -> Si basa su interfaccia seriale RS-232. Una stazione che vuole trasmettere manda un segnale alla stazione master attivando il segnale Request To Send. Se il master può ricevere risponde con un segnale Clear To Send. Questa procedura si basa sull'handshake.
	- XON/XOFF -> usato per terminali vicini tra loro. La stazione primaria invia dati, vengono memorizzati e utilizzati. Quando la memoria si riempe viene mandato un carattere XOFF che impedisce l'invio di nuovi blocchi. Appena il DTE si libera manda un messaggio XON
	- Stop and Wait
	- ARQ -> Automatic Repeat ReQuest o Query. Protocollo Full Duplex che usa il concetto di finestra mobile per essere più efficiente. 
- Ambito relazioni ibride
	- HDLC
	- PPP
	- MPLS
- Ambito peer to peer
	- TDM
	- FDM
	- SDH
### La trasmissione Dati
Lo strato fisico deve trasportare dati. Questi sono
- digitali -> rappresentazione discreta
- analogici -> segnale intenso, continuo
Nei DTE si usa una rappresentazione digitale trascrivendo ogni dato in sequenze di 0 o1.
I dati vengono sottoposti a:
- conversione in un differente tipo di segnale digitale, con livello 0 o 1
- conversione in analogico (modulazione), quindi un segnale con diversi livelli di intensi

### Segnali Sinusoidali
E' un segnale che varia nel tempo secondo la legge $U = U sin (ωt+Φ)$ dove t è il tempo trascorso, ω velocità angolare e Φ lo sfasamento di fase. La curva descritta prende il nome di sinusoide
![[Pasted image 20251001125920.png]]
Questa curva rappresenta il valore del seno dell'angolo istante per istante che ruota in senso anti orario con velocita ω. Quindi Φ rappresenta l'angolo che viene formato con l'asse x all'istante 0.

Ruotando tornerà alla posizione di partenza e si ripeterà. Il numero di volte al secondo che il segnale torna allo stato di partenza, si chiama frequenza e viene calcolata in $Hertz = 1/t$.

Un segnale che ha una frequenza di $1KHz$ vuol dire che percorrerà la circonferenza 1000 volte al secondo. La velocità è data dunque da $2\pi f$. Il periodo che sta nel nel mezzo della ripetizione del segnale si chiama periodo.

Un periodo è dato dall'unità di tempo diviso la frequenza -> $T=1/f$.
Dunque un segnale con $1Khz$ di frequenza ha periodo di $1/1000$ = 1 millisecondo.
La **lunghezza d'onda** $\lambda$ mette in relazione frequenza e velocità di trasmissione
$\lambda = C/f$ dove $C = 300.000 Km/sec$

Lo spettro è l'insieme di frequenze che il segnale contiene.
La larghezza di banda è l'intervallo delle frequenze contenute in un segnale composto. Se un segnale ad esempio trasmette da 300Hz a 3400Hz la sua larghezza sarà 3100Hz.

### Sviluppo in serie di Fourier

