# SQL - spørringer

Structured Query Language

Dette er en kort oversikt over de vanligste spørringene vi kan kjøre mot en database.

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
  kundeid INT NOT NULL,
  FOREIGN KEY (kundeid) REFERENCES kunde(kundeid)
);

CREATE TABLE linje
(
  linjeid serial primary key,
  pris INT NOT NULL,
  antall INT default 1,
  bestillingid INT NOT NULL,
  vareid INT NOT NULL,
  FOREIGN KEY (bestillingid) REFERENCES bestilling(bestillingid),
  FOREIGN KEY (vareid) REFERENCES vare(vareid)
);
```

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
