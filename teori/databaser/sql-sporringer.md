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
  from forfatter f join bok b
  on (f.forfatterid = b.forfatterid);
-- merk at "inner join" og "join" er synonymer
```

### Where betingelser

De fleste spørringer kan ende med en betingelse - en test som må oppfylles for at spørringen skal utføres.  
Dette gjelder ikke **insert** spørringer.

```sql
-- slettespørringer med where
--  tegnet ~ kan leses som "inneholder"
delete from forfatter where fornavn ~ 'ole';
-- update med where
update forfatter set kjonn = 'm' where fornavn = 'anne';
-- select med where
select fornavn, etternavn from forfatter where kjonn = 'm';
-- select med utvida where
select fornavn, etternavn from forfatter where kjonn = 'm' and fornavn ~ 'anne';
-- finner alle forfattere som er menn og har fornavn som inneholder "anne"

-- spørring med inner join og where
select f.fornavn, f.etternavn, b.tittel 
  from forfatter f inner join bok b
  on (f.forfatterid = b.forfatterid)
  where b.antallsider > 100;
-- finner fornavn,etternavn,tittel på forfatter/bok på over 100 sider

```

### Aggregatfunksjoner og subselects

I en spørring kan du bruke aggregat-funksjoner som kan beregne count, sum, avg, min og max.  
Dersom du vil finne antallet bøker med tittel som inneholder ordet "fred" kan du kjøre denne:  
`select count(*) from bok where tittel ~ 'fred';`  
For å få en finere kolonne-overskrift kan du bruke **as** til å sette navn på verdien:  
`select count(*)`**`as`**`antall from bok where tittel ~ 'fred';`  
De andre aggregat-funksjonene \(sum,min,max,avg\) brukes på tall-felt.

```sql
-- hvor lang er den lengste boka ?
select max(antallsider) from bok;

-- Versjon 1: hvem har skrevet den lengste boka ?
-- denne bruker subselect
-- MERK: denne feiler dersom det er fler som har lengst bok
select fornavn,etternavn from forfatter 
       where forfatterid =  
       (select forfatterid from bok where antallsider = 
         (select max(antallsider) from bok) 
        );

-- Versjon 2: hvem har skrevet den lengste boka ? 
-- takler flere vinnere
-- MERK: skifter "=" til "in"
select fornavn,etternavn from forfatter 
       where forfatterid in  
       (select forfatterid from bok where antallsider = 
         (select max(antallsider) from bok) 
        );
        
-- hvor lange er astrid lingrens bøker i gjennomsnitt ?
-- versjon 1, vi kjenner forfatterid til astrid
select avg(antallsider) from bok where forfatterid = 22;

-- versjon 2 - vi kjenner ikke forfatterid        
select avg(antallsider) from bok 
  where forfatterid =
  (select forfatterid from forfatter where 
        fornavn='Astrid' and etternavn='Lindgren');
-- merk at her må fornavn/etternavn matche eksakt
-- "astrid" er ikke lik "Astrid"
-- dersom flere har dette navnet må vi skifte til "in" som på linje 17
```

### Aggregatfunksjoner med group by og having

Vi kan gruppere resultatene av en aggregatfunksjon med **group by**, og filtrere med **having**.

```sql
-- hvor mange sider har hver forfatter skrevet tilsammen ?
select f.fornavn, f.etternavn, sum(b.antallsider) as total from 
       forfatter f join bok b on (b.forfatterid=f.forfatterid) 
       group by f.forfatterid;
-- får kolonner: fornavn,etternavn,total

-- hvilke forfattere har skrevet minst 500 sider tilsammen ?
select f.fornavn, f.etternavn, sum(b.antallsider) as total from 
       forfatter f join bok b on (b.forfatterid=f.forfatterid) 
       group by f.forfatterid having sum(b.antallsider) > 500;
-- merk at jeg ikke kan skrive "having total > 500", må gjenta beregningen
```

### Begrens antall rader

```sql
-- dersom du bare vil ha noen få rader kan du bruke limit
select * from bok order by antallsider limit 1;
-- finner boka med flest sider (bare en)
```

