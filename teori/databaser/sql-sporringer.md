# SQL - spørringer

Structured Query Language

Dette er en kort oversikt over de vanligste spørringene vi kan kjøre mot en database.

### Create table

```sql
# vi antar at vi har laga følgende tabeller
CREATE TABLE kunde
(
  kundeid serial primary key,
  fornavn text not null,
  etternavn text not null,
  adresse text not null,
  tlf text default '',
  epost text default ''
);

CREATE TABLE vare
(
  vareid serial primary key,
  varenavn text not null,
  beholdning INT default 0,
  basispris INT NOT NULL
);

CREATE TABLE bestilling
(
  bestillingid serial primary key,
  dato DATE NOT NULL,
  betalt boolean default false,
  betalingsmetode text not null,
  kundeid INT REFERENCES kunde(kundeid)
);

CREATE TABLE linje
(
  linjeid serial primary key,
  pris INT NOT NULL,
  antall INT default 1,
  bestillingid INT REFERENCES bestilling(bestillingid),
  vareid INT REFERENCES vare(vareid)
);
```

### insert update delete

Ved å kjøre disse sql-linjene har vi laga tabellene kunde, vare, bestilling og linje.  
Vi kan nå legge inn data i tabellene:

```sql
insert into vare (varenavn, basispris) values 
 ('ost',12), ('brød',17), ('melk',22),
 ('brunost',12), ('winerbrød',17), ('surmelk',12),
 ('gulost',12), ('grovbrød',37), ('lettmelk',32);
update vare set beholdning = 12;   # alle får beholdning = 12
update vare set beholdning = 3 where varenavn = 'ost';  # vi har 3 ost
select * from vare;  # viser alle varer
select varenavn,beholdning from vare;  # alle varer, men bare to felt
select * from vare where basispris > 10; # alle varer over 10 kr
delete from vare where varenavn = 'ost'; # sletter en linje
delete from vare where beholdning = 12; # sletter mange

```

### Inner join

Noen ganger trenger vi felt fra flere tabeller.   
Anta at vi har laga en datamodell for et bibliotek som vist under:

```sql
CREATE TABLE laaner (
  laanerid serial primary key,
  fornavn text not null,
  etternavn text not null,
  adresse text,
  epost text,
  tlf text,
  kjonn text
);

CREATE TABLE forfatter (
  forfatterid serial primary key,
  fornavn text not null,
  etternavn text not null,
  fdato date,
  kjonn text check (
    kjonn = 'm'
    or kjonn = 'f'
  )
);

CREATE TABLE bok (
  bokid serial primary key,
  tittel text not null,
  pdato date,
  isbn text,
  antallSider int check (antallsider > 0),
  sjanger text,
  spraak text,
  forfatterid int references forfatter (forfatterid)
);

CREATE TABLE eksemplar (
  eksemplarid serial primary key,
  tillstand text,
  bokid int references bok (bokid)
);

CREATE TABLE utlaan (
  utlaanid serial primary key,
  udato date,
  innlevert text default 'nei' check (
    innlevert = 'ja'
    or innlevert = 'nei'
  ),
  laanerid int references laaner (laanerid),
  eksemplarid int references eksemplar (eksemplarid)
);
```

For å vise en liste over forfattere med bøkene de har skrevet med feltene  **fornavn, etternavn og tittel**  
må vi lage en spørring som limer sammen tabellene forfatter og bok.  
I sql kalles dette en inner join og krever at tabellene har et koblingsfelt \(i dette tilfellet er det forfatterid\) som finnes i begge tabellene.

```sql
select fornavn,etternavn,tittel from 
   forfatter inner join bok
   on (forfatter.forfatterid = bok.forfatterid);
   
-- ofte nyttig å gi et kortnavn til tabellen slik som dette:
select f.fornavn, f.etternavn, b.tittel 
  from forfatter f inner join bok b
  on (f.forfatterid = b.forfatterid);
```



