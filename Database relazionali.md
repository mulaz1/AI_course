b## Database Relazioneli

### Sistema informativo
. Informazioni di interesse nei processi aziendali
. Modalità in cui esse sono gestite
. Risorse coinvolte, sia umane sia tecnologiche

### Gestione dei dati

* __Ridondanza__        -> Più copie dello stesso dato
* __Inconsistenza__     -> Copie modificate diversamente
* __Riservatezza__      -> Dati riservati accessibili a persone non autorizzate
* __Integrità__         -> operazioni sbagliate o incomplete sui dati
* __Concorrenza__ -> accesso e aggiornamento dati non sincronizzato tra programmi differenti

### Gestione Condivisione Dati

* > Tutte le azioni/operazioni sui dati vengono gestite da dei __DBMS__  ( database management system )
* Controlli su:
  * Ridondanza, consistenza, distribuzione
  * Riservatezza, integrità
  * Accesso concorrente

### Quando segliere un DBMS

* Quando si trattano di __GRANDI__ dimensioni (fino e oltre Tbyte)
* Quando sono __CONDIVISI__ e si hanno accessi diversi da app e utenti diversi
* Quando e' __PERSISTENTE__ quando il tempo di vita > dell'esecuzione dell'app

### Quando evitarlo

Quando si hanno :
* Insieme dati piccolo e semplice
* Poche modifiche nel tempo
* Non condiviso
* Prestazioni in tempo reale

## Accesso concorrente

> Problemi di consistenza dei dati condivisi

Esempio: 

Prelievo da un conto corrente come sequenza operazioni
. Verifica disponibilità
. Sottrazione importo

Questa operazione si chiama __Transazione__:
* Insieme di operazioni non decomponibili
  * > Eseguite completamente, prima che stessi dati siano nuovamente disponibili __ACID__ ( atomicity, consistency, isolation, durability )

### Architettura a 3 livelli

![](/images/image1.png)

### Linguaggi DDL e DML

* > __DDL__ ( Data Definition Language ),  intensionale
  * Usato dal DBA (amministratore)
  * Definire lo schema dati, secondo il modello concettuale: gerarchico, relazionale ecc.
  * Usato per definire tabelle, campi, chiavi ecc.
</br>
* > __DML__ ( Data Manipulation Language ),  estensionale
  * Usato all'interno delle applicazioni
  * __SQL__(INSERT, SELECT, UPDATE, DELETE)
  * 4 metodi HTTP (POST, GET, PUT, DELETE)


## Un po' di storia...

### Modello relazionale
* >Codd - 1970; DBMS reali - 1981
  * Si basa sul concetto matematico di relazione 
  * Relazioni rappresentate da familiari 
* > A ciascun __DOMINIO__ e' associato un nome unico nella relazione
  * Il nome “descrive” il ruolo del dominio
  * Attributi usati come intestazioni delle informazioni inserite nella __ROW__ della tabella 

### Definizione di Relazione

* Relazione R: insieme di n-uple ordinate (d1 … dn) tali che d1 ϵ D1 ... dn ϵ Dn
* R è sottoinsieme del prodotto cartesiano D1 × D2 × … × Dn
* Insiemi D1 … Dn (anche non distinti) detti __DOMINI__
* Valore n detto __GRADO__ di R
* Il numero di n-uple in R è detto __CARDINALITA'__ di R

![esempio di database relazionale](/images/image2.png)

### terminologia

![](/images/image3.png)

### Dominio di un attributo

* Tuple di una relazione definite dall'insieme dei valori corrispondenti agli attributi
* __Dominio__ di un attributo: insieme di tutti e soli i valori che quell'attributo può
assumere

### Modello E-R
* Si creano associazioni tra entità distinte, tramite condivisione di attributi
   *  Le righe di diverse tabelle hanno domini in comune
* Semplicità: forza del modello relazionale!

## Termini e Metodonimia

### Chiave primaria

* Una tabella (relazione) non dovrebbe contenere due righe identiche
* Minimo sottoinsieme di campi che permette di Identificare univocamente le righe della tabella
* Ciascuna riga della tabella identificata univocamente __Chiave primaria__ di una tabella

### Chiave esterna

* Le informazioni presenti in tabelle diverse possono essere associate tra loro
perché tali tabelle hanno dei domini in comune
* Quando il dominio di un campo K che è chiave primaria in una tabella A è presente anche in un’altra tabella B, allora questo campo K è detto chiave esterna verso la tabella A

### Concetto e tipo di __CHIAVE__

![](/images/image4.png)

### Chiave candidata

* Le chiavi candidate sono gli attributi in una relazione con la proprietà di poter
essere la chiave primaria:
    * Tra le chiavi candidate deve essere scelta la chiave primaria
    * Le chiavi escluse si dicono chiavi alternative
* Le righe di una tabella rappresentano “entità” del mondo reale
* La chiave primaria rappresenta il modo con cui è possibile distinguere queste entità

### Normalizzazione

> Processo di organizzazione dei dati per evitare __ridondanza__, __anomalie__,
__inefficienza__
* Stessa informazione in più copie → svantaggio
* Maggio uso di memoria 
* Ripetizione della stessa informazione


### Prima forma normale 
* La relazione rispetta il modello relazionale
* Le tuple hanno un numero fisso di attributi definiti su domini elementari
* Caratteristiche:
  * Non ci sono __righe uguali__
  * __Atomicità:__ solo attributi elementari
  * Non ci sono attributi __ripetitivi__

![](/images/image5.png)

### Seconda forma normale
* Non ci sono attributi non-chiave che dipendono parzialmente dalla chiave

### Terza forma normale
* Non ci sono attributi non-chiave che dipendono __transitivamente__ dalla chiave
  * Ossia dipendenti da campi non-chiave


## Operatori relazionali

* Base teorica per i linguaggi di interrogazione delle basi di dati relazionali
* Operano su intere tabelle considerate come insiemi, piuttosto che record
per record
* Operatori
  * __Unione__, __intersezione__, __differenza__ 
  * __Selezione__, __proiezione__
  * __Prodotto cartesiano__, __join__


### Create, select

```sql 

create table Table (
Attribute Domain [Constraints],
Attribute Domain [Constraints]
…
[OtherConstraints]
)
select Attribute, Attribute …
from Table, Table …
[where Conditions]

```

### Insert, update, delete

```sql 

insert into Table [(Attributes)] values(Values)
insert into Table [(Attributes)] select …
update Table set Attribute = <Expression | select … | null | default> [where Condition]
delete from Table [where Condition]
```
## Esempi 

### Ricerche semplici

> Usando semplici operazioni in sql 
* Seleziona name e income delle persone con eta' minore di 30 anni, dalla tabella Person 
* Seleziona tutti i campi di tutte le persone con eta' minore di 30 anni dalla tabella Person
* 

``` sql

select Name, Income from Person where Age < 30
select * from Person where Age < 30
select Paternity.Father
    from Person
    join Paternity
    on Paternity.Child = Person.Name
    where Person.Income > 50

```
###  Manipolazione dati

```sql
insert into Person values ('Mario', 25, 52);
insert into Person (Name, Age) values ('Pino', 25);
delete from Person where Age < 18;
update Person set Income = 45 where Name = 'Piero';
update Person set Income = Income * 1.1 where Age < 30;

```

### Ricerche complesse

```sql 

select C.Name, C.Income, F.Age
from Person C
join Paternity P on C.Name = P.Child
join Person F on F.Name = P.Father
where C.Income > F.Income;
select Paternity.Child, Father, Mother
from Paternity
join Maternity on Paternity.Child = Maternity.Child

```