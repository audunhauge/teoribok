# Databaser

## PostgresSQL

Postgres er en database-server som vi kan installere på egen maskin eller på en hosted-server.  
Etter at den er satt opp riktig kan vi starte opp pgsql \(kommandovindu\) 

### Lage en ny database

```sql
CREATE DATABASE bib;
```

Legg merke til at linja slutter med semikolon, ingenting skjer dersom denne ikke er med.

Fra postgres.app kan vi nå åpne den nye databasen

Deretter bruker vi erdplus.com til å lage en databasemodell for tabellen **bok** og tabellen **forfatter**.  
Modellen eksporteres som SQL som vi så limer inn i kommandovinduet.

```sql
CREATE TABLE forfatter
(
  forfatterID INT NOT NULL,
  navn CHAR(30) NOT NULL,
  PRIMARY KEY (forfatterID)
);

CREATE TABLE bok
(
  bokID INT NOT NULL,
  isbn CHAR(20) NOT NULL,
  tittel CHAR(60) NOT NULL,
  antallSider INT NOT NULL,
  forfatterID INT NOT NULL,
  PRIMARY KEY (bokID),
  FOREIGN KEY (forfatterID) REFERENCES forfatter(forfatterID),
  UNIQUE (isbn)
);
```

Vi bruker kommandoen \d til å vise hvilke tabeller vi har.  
Vi kan også sjekke tabellen bok med \d bok   \(definisjon av bok\).

### Legge inn data \(insert-spørring\)

Vi kan nå registrere \(legge inn\) forfattere på denne måten:

```sql
insert into forfatter (forfatterID, navn) values (1,'ole olsen');
# merk at vi MÅ bruke hermetegnet '  du kan ikke bruke "
# legg inn flere forfattere ved å trykke pil opp og så rediger verdiene
# merk at alle forfatttere må ha sitt eget forfatterID

# vi kan velge ut alle forfattere fra tabellen slik:
select * from forfatter
# viser alle registrerte forfattere
```

### Velge ut data \(spørring\)

```sql
select * from forfatter where navn ~ 'ole';
// finner alle forfattere som har navn som ligner på 'ole'

select isbn,antallSider from bok where tittel ~ 'krig';
// alle isbn til bøker som inneholder 'krig' i tittelen
```

### Slette data \(slette-spørring\)

```sql
delete from forfatter where navn ~ 'ole';
// sletter alle forfattere som har navn som ligner på 'ole'

delete from bok where tittel ~ 'krig';
// sletter alle bøker som inneholder 'krig' i tittelen
```

### Velge fra to tabeller \(inner join\)

```sql
select b.tittel, f.navn from bok b inner join forfatter f 
       on (b.forfatterid = f.forfatterid)
       where b.tittel ~ 'krig';
// finner tittel,forfatternavn for alle bøker 
// som har en tittel som inneholder 'krig'       
```

For å koble sammen to tabeller i en spørring bruker vi **inner join**.  
Spørringen kobler sammen tabellene bok og forfatter \(de har en relasjon\) og finner verdiene som hører sammen.

