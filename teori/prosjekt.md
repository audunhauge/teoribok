# Prosjekt

### Lag en database for prosjektet

Se [oppskrift](databaser/#lag-en-ny-database) på hvordan du lager en ny database.  
Du må endre litt på kommandoene   
`create role bib password '123';`  
må redigeres til  `create role xxx password 'yyy';`

Gjør det samme for begge\[sic\] de tre linjene. Linjene skal kjøres i postgres.  
Lag en prosjektnavn.sql for databasen i vs-code. Denne kan du importere i dbdiagram.io og sjekke  
om den virker. Når den er i orden kan du kjøre den i postgres -  
startes med `psql databaseNavn -U databaseEier` \(psql bib -U bib for forrige prosjekt\).  
Lim inn koden fra prosjektnavn.sql i dette vinduet. Da lages tabellene.

```sql
-- Jeg la inn linjene under i mitt forsøk: shop.sql
-- Dette fikser eierskap på alle tabellene mine.
-- Endre til dine tabellnavn og ditt brukernavn.
alter table bestilling owner to shop;
alter table vare owner to shop;
alter table kunde owner to shop;
alter table linje owner to shop;
```

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
public
  |------
     // her ligger websider som alle kan se
     // du trenger ikke logge inn
     index.html    --- må være med, dette er startsida
admin
  |------
     her ligger admin sider som er beskytta av passord
     og sider som krever vanlig brukernavn
```

Filen app.js må redigeres - endre   
`const CONNECTSTRING = "postgres://bib:123@localhost/bib";`  
til riktig versjon for ditt prosjekt. Bytt ut bib med den nye brukeren du laga tidligere.  
Strukturen er:  postgres://brukernavn:passord@server/databasenavn

### Første testkjøring

Når databasen er laga, app.js er redigert og mappestrukturen er som vist - da kan du kjøre første test:.

* [ ] Høyre-klikk på app.js og velg **open in terminal**.
* [ ] Skriv `npm install`.
* [ ] Skriv `node app.js` .

Med litt flaks skriver serveren ut   
`Du kan koble deg til på` [`http://localhost:3000`](http://localhost:3000)

Den sida som vises er public/index.html. Dette er forsida til prosjektet ditt og skal inneholde overskrift, bilder og anna snadder. I tillegg linker til admin-sider og andre sider som bruker databasen.

