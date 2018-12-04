# Uke 42

## Installasjon av postgresSQL

Denne uka jobber vi med å installere postgres. Postgres er en database-server som støtter hele SQL standarden. På mac installerer vi postgres.app \(link til inst-side\)  
På windows installerer vi postgres fra \(link til installasjons-sida\).

Etter installasjon starter vi opp et kommandovindu slik at vi kan skrive inn SQL kommandoer.

\(kort framgangsmåte for win/mac\)

På mac åpner vi den eksisterende databasen **postgres** .

Vi skriver inn følgende SQL for å lage en ny, tom database:

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



