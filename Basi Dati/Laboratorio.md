### Linguaggio SQL
Funzionalità:
- Data Definition Language -> permette di lavorare con strutture dati e vincoli di integrità (CREATE, ALTER, DROP, RENAME, TRUNCATE, ...)
- Data Manipulation Language -> Consente di manipolare i dati (SELECT, INSERT, UPDATE, DELETE, ...)
- Data Control Language -> Gestisce privilegi (GRANT, REVOKE)
- Transaction Control Language -> Permette di gestire transizioni come validazione e annullamento delle modifiche (COMMIT, SAVEPOINT, ROLLBACK, SET TRANSACTION)
- Embedded SQL -> permette integrare comandi SQL nel linguaggio ospite (C++, Java)

### DBMS Basato su SQL
Consente di gestire basti dati relazionali. Quando ci si connette si deve specificare la base dati sulla quale si vuole operare.

![[astrazione.png]]

### Definizione Schema
Permette di dividere logicamente la base dati ed è identificato da un nome di schema.
Es. `CREATE SCHEMA Ditta`
La sintassi è `CREATE SCHEMA <nome_db> [AUTHORIZATION<nome_prop>]`
Dopo lo schema vi può essere un'autorizzazione per indicare propietario o definire le tabelle.

Dopo la sua creazione si possono aggiungere oggetti:
`CREATE DOMAIN Ditta.dom_stipendio AS NUMERIC(8, 2) CHECK VALUE ≥ 900;`
`CREATE DOMAIN Ditta.dom_cod_impiegato AS VARCHAR(4);`
`CREATE TABLE Ditta.Impiegato ( cod Ditta.dom_cod_impiegato PRIMARY KEY, nome varchar(40) NOT NULL, stipendio Ditta.dom_stipendio );`

Lo schema in genere è specificato implicitamente da dove vengono usate le istruzioni `CREATE`. In questo caso no è necessario specificare il nome dello schema.
`CREATE TABLE Impiegato ( cod dom cod impiegato PRIMARY KEY, nome varchar(40) NOT NULL, stipendio dom stipendio );`

### Schema predefinito PostgreSQL
In Postgre esiste uno schema predefinito public
`CREATE TABLE R (a CHAR PRIMARY KEY, b CHAR);` equivale a `CREATE TABLE public.R (a CHAR PRIMARY KEY, b CHAR);`

Sintassi del CREATE TABLE:
![[sintassiCreate.png]]

### Domini
- Elementari
	- Carattere -> singoli caratteri o stringe
	- Bit -> flag booleani o stringhe
	- Domini numerici -> esatti ed approssimativi
	- data, ora, intervalli di tempo
- Definiti dall'utente -> si creano con `CREATE DOMAIN <nome> AS CHAR(2) NOT NULL`

### Vincoli Intrarelazionali
- Integrità -> devono essere soddisfatti da ogni istanza di relazione della base di dati (`NOT NULL, UNIQUE, PRIMARY KEY, CHECK(condizione)`)
Coinvolgono più relazioni tipo ad esempio i vincoli di integrità referenziale o di riferimento.

La SQL definisce due funzioni per definire chiavi esterne:
- `FOREIGN KEY` -> definizione di chiavi esterne su più attributi
- `REFERENCE` -> definizione di chiavi esterne su un attributo
` nome_var_red VARCHAR(x) REFERENCES tabellla(var_tabella)`

# Esercizi
### Q1
Donne in gara 
$\pi(\rho(artista)(nazione = IT, sesso=F))nome$
### Q2
Artisti polacchi con film in proiezione
$\sigma(\sigma[(artista)x(film)](nome=regista)=(nazione=POL)$