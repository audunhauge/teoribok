# Prosjekt

### Opprett en felles github

En på gruppa lager en ny repository på github.  
Klikk på det nye repositoriet \( i github.com\) og velg **settings**.  
Under **options** vil du se **collaborators**, klikk på denne.  
Skriv in brukernavn \(på github\) for de som skal være med i prosjektet.

### Last ned det nye prosjektet

Gå inn på repositoriet \(på github.com\), klikk på navnet og du skal se en grønn knapp med  
**clone or download** som tekst. Klikk på denne og velg https - ta kopi av linken.  
Åpne **terminal** og skriv inn følgende: \(men med den kopierte linken\)  
`git clone` [`https://github.com/brukernavnetDitt/prosjektnavn.git`](https://github.com/audunhauge/studietid.git)\`\`

### Kopier sikkert-bibliotek

Bruk vs-code til å å sjekke at du har siste versjon av audunhauge.github.io \(git pull\).  
Kopier innholdet av Sikkert-bibliotek til den nye prosjektmappa \(den du fikk med git clone\).  
Gå inn i mappa \(bruk vs-code\). Du skal se samme struktur som i Sikkert-Bib.  
Merk at følgende filer MÅ VÆRE MED:

* app.js
* package.json
* public/  \(en mappe\)
* public/index.html   \(startsida\)
* admin/  \(en mappe\)

```text
app.js          --- må være med
package.json    --- må være med
xxx.sql         --- skal være med (xxx => prosjektnavn)
public
  |------
     // her ligger websider som alle kan se
     // du trenger ikke logge inn
     index.html    --- må være med, dette er startsida
     plan.html     --- plandokument for prosjektet
admin
  |------
     her ligger admin sider som er beskytta av passord
     og sider som krever vanlig brukernavn
```

Filen app.js må redigeres - endre   
`const CONNECTSTRING = "postgres://xxx:123@localhost/xxx";`  
til riktig versjon for ditt prosjekt. Bytt ut xxx med den nye brukeren du lager for prosjektet.  
Strukturen er:  postgres://brukernavn:passord@server/databasenavn

### Lag en database for prosjektet

Under en grovskisse til xxx.sql \(xxx byttes ut med prosjektnavnet deres\).  
**Merk at tabellen** _**users**_ **må finnes dersom nye brukere skal kunne registrere seg selv.**  
Ta kopi og rediger filen under, legg den på samme nivå som app.js i prosjektet.  
Åpne en terminal \(ctrl+klikk på app.js, velg Open in terminal\) og start opp postgres \(skriv psql\).  
Skriv denne kommandoen i psql:  `\i xxx.sql` \(igjen:  xxx.sql er navnet på fila under, xxx byttes ut\).  
Da lastes denne fila inn og alle kommandoene kjøres.  
**Alternativt** kan du starte postgres.app, åpne postgres databasen og paste inn innholdet under.

{% tabs %}
{% tab title="SQL" %}
{% code title="xxx.sql" %}
```sql
-- lag database,bruker og set passord
-- kan gjøres fra postgres databasen i postgres.app

create role xxx password '123';     -- xxx er brukeren
alter role xxx with login;          -- kan logge in via net
create database xxx owner xxx;      -- lag en database xxx

-- skift til den nye databasen
\c xxx;

--- viser eksempel for en webshop
--- ALLE SKAL HA MED USERS 

DROP TABLE IF EXISTS users cascade;
DROP TABLE IF EXISTS kunde cascade;
DROP TABLE IF EXISTS vare cascade;
DROP TABLE IF EXISTS bestilling cascade;
DROP TABLE IF EXISTS linje cascade;


create table users (
    userid SERIAL PRIMARY KEY,
    username text unique not null,
    email text unique not null,
    role text default 'user',
    password text not null
);

--- denne tabellen inneholder ekstrafelt
--- users er det som MÅ FINNES
CREATE TABLE kunde (
  kundeid SERIAL PRIMARY KEY,
  fornavn text NOT NULL,
  etternavn text NOT NULL,
  adresse text,
  epost text,
  tlf text,
  kjonn text,
  userid int unique not null
);

CREATE TABLE  vare  (
   vareid  SERIAL PRIMARY KEY,
   navn  text NOT NULL,
   pris  int NOT NULL
);

CREATE TABLE  bestilling  (
   bestillingid  SERIAL PRIMARY KEY,
   dato  date NOT NULL,
   kundeid  int NOT NULL
);

CREATE TABLE  linje  (
   linjeid  SERIAL PRIMARY KEY,
   antall  int DEFAULT 1,
   vareid  int NOT NULL,
   bestillingid  int NOT NULL
);

ALTER TABLE  bestilling  ADD FOREIGN KEY ( kundeid ) 
      REFERENCES  kunde  ( kundeid );
ALTER TABLE  linje  ADD FOREIGN KEY ( bestillingid ) 
      REFERENCES  bestilling  ( bestillingid );
ALTER TABLE  linje  ADD FOREIGN KEY ( vareid ) 
      REFERENCES  vare  ( vareid );
ALTER TABLE  kunde  ADD FOREIGN KEY ( userid ) 
      REFERENCES  users  ( userid );
      

-- sørg for at bruker xxx eier alle tabellene
alter table users owner to xxx;
alter table bestilling owner to xxx;
alter table vare owner to xxx;
alter table kunde owner to xxx;
alter table linje owner to xxx;
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Første testkjøring

Når databasen er laga, app.js er redigert og mappestrukturen er som vist - da kan du kjøre første test:.

* [ ] Høyre-klikk på app.js og velg **open in terminal**.
* [ ] Skriv `npm install`.
* [ ] Skriv `node app.js` .

Med litt flaks skriver serveren ut   
`Du kan koble deg til på` [`http://localhost:3000`](http://localhost:3000)

Den sida som vises er public/index.html. Dette er forsida til prosjektet ditt og skal inneholde overskrift, bilder og anna snadder. I tillegg linker til admin-sider og andre sider som bruker databasen.

