# Database skjema

## Installasjon av node og npm

Søk på _install nodejs mac_ og installer \([https://nodejs.org/en/download/](https://nodejs.org/en/download/)\).  
Du gjør det samme for windows \(windows har kjøpt både nodejs og github\).  
Etter installasjon kan du åpne et nytt kommandovindu \(se win/mac under\) og teste:

{% tabs %}
{% tab title="På mac" %}
```text
I søkefeltet skriver du terminal - velg terminal.app

:~ bruker$  node
Welcome to Node,js vxx.xxx
Type .help for more information
// trykk ctrl+d for å avslutte node

Sjekk at npm også virker (antar du har avslutta node)
:~ bruker$  npm
Usage: npm <command>
.... masse tekst
```
{% endtab %}

{% tab title="Windows" %}
```
I søkefeltet skriver du power shell og starter programmet.

c:\xxx\xxx   node.exe
Welcome to Node,js vxx.xxx
Type .help for more information
// trykk ctrl+d for å avslutte node

Sjekk at npm også virker (antar du har avslutta node)
c:\xxx\xxx  npm.exe
Usage: npm <command>
.... masse tekst
```
{% endtab %}
{% endtabs %}

Dersom begge programmene er på plass - da kan vi gå inn i vs-code og åpne mappa med bibliotek prosjektet. Lag en ny mappe med navnet **public** \(på samme nivå som bib.sql\).  
Lag en ny fil med navnet package.json med innholdet:

```javascript
{
  "name": "webserver",
  "version": "1.0.0",
  "description": "server for bib",
  "main": "app.js",
  "author": "navnet ditt",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.4",
    "pg-promise": "^8.5.1"
  }
}
```

Lag en ny fil med navnet **app.js** og lim inn innhold:

{% tabs %}
{% tab title="app.js" %}
```javascript
// @ts-check

const CONNECTSTRING = "postgres://bib:123@localhost/bib";

const PORT = 3000;

const express = require("express");
const pgp = require("pg-promise")();
const db = pgp(CONNECTSTRING);

const app = express();
const bodyParser = require("body-parser");


app.use(express.static("public"));
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// Define routes.
app.get("/", function (req, res) {
  res.send({ msg: "ok" });
});

app.post("/runsql", function (req, res) {
  let data = req.body;
  runsql(res, data);
});

app.listen(3000, function () {
  console.log(`Node server started on port ${PORT}`);
});

async function runsql(res, obj) {
  let results;
  let sql = obj.sql;
  let data = obj.data;
  await db.any(
    sql,data
  )
    .then(data => {
      results = data;
    })
    .catch(error => {
      console.log("ERROR:", sql, ":", error.message); // print error;
      results = {};
    });
  res.send({ results });
}
```
{% endtab %}
{% endtabs %}

### Start av node server

I visual studio code kan du nå høyre-klikke \(ctrl+venstre osv\) på filen app.js og velge  
**Open in terminal** . Du får nå opp en integrert terminal i vs-code.  
Sjekk at vi er i riktig mappe ved å skrive   
**ls** og du skal se mappa **public** og filene _**app.js, bib.sql** og **package.json**_ .

Skriv **npm install** i terminalvinduet for å legge til nødvendige node filer til prosjektet.  
DETTE MÅ DU GJØRE HVER GANG DU STARTER ETT NYTT NODE PROSJEKT.  
Nå kan du teste at serveren virker ved å skrive  
**node app.js**   
Du skal se  
**Node server started on port 3000**

### **Testing av en enkel html fil**

For å teste serveren lager vi en **test.html** i mappa **public**.  
Lag filen test.html, skriv inn ! og legg inn &lt;h1&gt;hello world!&lt;/h1&gt;.  
Lagre filen og deretter åpner vi en nettleser på adressen **localhost:3000/test.html** .

## Web-skjema kobla til databasen

Kopier inn filene i public mappa fra [min versjon](https://github.com/audunhauge/audunhauge.github.io/tree/master/it1/Bibliotek/public) på github.  
Merk at de **SKAL** ligge i public mappa.  
I nettleseren kan du nå åpne localhost:3000/forfatter.html og du bør se en side som under:  
\(bortsett fra at den viser forfatter - ikke låner\).  
Lag filene eksemplar.html og laaner.html ut fra eksemplene \(copy/paste\).  
Du må redigere litt for å få dem til å virke.

![forfatter](../../.gitbook/assets/forfatter.png)

### Hovedskjema og underskjema med custom components

Jeg har laga følgende custom components som gjør det enklere å lage et skjema som er kobla til databasen. Du bør ta "pull" på min github for å sikre deg at du har siste versjon.  
Du finner komponentene i mappa [it1/SikkertBibliotek](https://github.com/audunhauge/audunhauge.github.io/tree/master/it1/SikkertBibliotek). Se i public/components.

### **DbTable** 

Denne komponenten brukes til å vise en tabell med poster fra en spørring. Spørringen kan være enkel, slik som "select \* from bok" eller inneholde join, group by osv. Kan også brukes til å slette valgte poster fra en tabell. Kan kombineres med db-insert og db-update \(synkronisert\).

Du trenger  &lt;script src="DbTable.js"&gt;&lt;/script&gt; i html-filen, kan legges i &lt;head&gt;  
Legg inn riktig sti \( i mine eksempler ligger html filene i mappa html, komponentene ligger i components, derfor må jeg skrive src="../components/DbTable.js"      ".." betyr gå opp ett mappenivå.\)

```markup
<db-table  update="bok" 
            delete="bok"
            fields="bokid:hidden,tittel,antallsider:number"
               sql="select * from bok"  >
        <span slot="caption"> Bøker </span>
</db-table>
```

update = bok   ---  fører til at tabellen lastes på nytt dersom tabellen bok endres av andre komponenter  
                                typisk bruk er at du har en db-insert og en db-table mot samme tabell på samme side.  
                                da vil lagring av ny bok trigge oppdatering av db-table.  
delete = bok    ---  du kan markere og slette poster \(sletter i tabellen bok\) - forutsetter at nøkkelfelt for  
                               tabellen bok er første felt i fields="..."  
fields                ---  list de feltene du vil vise, du kan bruke number,checkbox,date,hidden som felttype.  
                               :hidden gjør at feltet er med, men vises ikke   
                               \(trengs kanskje til å koble komponenter\)  
sql                     ---  skriv ønska sql, må returnere feltene som er nevnt i fields, kan bruke \*, all lovlig sql.    
slot=caption    ---  her kan du legge inn ønska overskrift for tabellen. Du kan style den med vanlig css.  
  
Selve &lt;db-table&gt; tar imot disse verdiene fra css:  { --head:beige;  --alternate:lightsteelblue; }

![Visning for &amp;lt;db-table&amp;gt; over](../../.gitbook/assets/dbtable.png)

### DbInsert

Denne komponenten lar deg registrere nye poster i en tabell. Støtter enkle fremmednøkler \(verdi hentes fra en annen tabell\). Dersom du ønsker/trenger en fremmednøkkel basert på en spørring, da kan du bruke   
**db-foreign** som en subkomponent. Typisk vil du ha med **db-table** på samme skjema/webside slik at bruker får god feedback på at innsetting var vellykka.

Koble til script som for db-table.

```markup
<!-- NR.1 enkel versjon -->
<db-insert id="f1" 
       fields="fornavn,etternavn" 
        table="forfatter"  >
   <span slot="heading">Registrer Forfatter</span>
</db-insert>

<!-- NR.2 flere fremmednøkler -->
<db-insert id="f2" 
       fields="innlevert:checkbox" 
      foreign="laaner.laanerid:fornavn+etternavn" 
        table="utlaan"  >
    <span slot="heading">Registrer Utlån</span>
    <db-foreign  label="tittel" 
               foreign="eksemplarid"
                   sql="select e.eksemplarid,
   concat(e.eksemplarid,':',b.tittel,' av ',f.fornavn, ' ',f.etternavn,
          ', tillstand:',e.tillstand) as tittel 
   from eksemplar e join bok b on (e.bokid = b.bokid) 
   join forfatter f on (f.forfatterid = b.forfatterid)"  >
     </db-foreign>
</db-insert>
```

Det første eksemplet er rett fram, en tabell uten fremmednøkler er lett å sette opp.

Eksempel nr 2 har to fremmednøkler, laanerid og eksemplarid.  
Fremmednøkkelen for **laanerid** kan lages ved hjelp av  
  foreign="laaner.laanerid:fornavn+etternavn"  
laaner.laanerid sier at vi henter laanerid fra tabellen laaner - dette gir verdi til fremmednøkkelen.  
:fornavn+etternavn sier at vi ønsker å vise navn på låner i kombo-boksen, ellers vil bare laanerid vises.  
Fremmednøkkelen for **eksemplarid** kan ikke lages så enkelt, da tabellen eksemplar ikke har tittel på bok eller navn på forfatter \(som vi nesten må vise\). Dermed bruker vi komponenten db-foreign som lar oss sette sammen en komboboks basert på en spørring. Sjekk nedenfor hvordan du kan bruke **db-foreign** .

### DbForeign

Denne komponenten lar deg lage en komboboks \(&lt;select&gt;\) basert på en spørring.

label="navn"     teksten som vises som label for &lt;select&gt;  
foreign="felt"    feltet som skal få verdi fra denne komponenten  
sql = "..."            sql som velger verdier for &lt;select&gt;, både felt som gir verdi til fremmednøkkel og felt som  
                           skal brukes til å vise valg i comboen må tas med.

Ved change i denne komponenten sendes en custom event dbChange med id på &lt;select&gt;.  
Intereserte komponenter \(slik som dbinsert\) kan da hente ut verdien.

![Tittel er laga med db-foreign, laaner er laga av db-insert](../../.gitbook/assets/dbforeign.png)

### DbUpdate

Denn komponenten lar deg redigere poster som allerede er registrerte. Passer også godt til å lage hoved-underskjema. Underskjema er da laga med db-table som oppdateres når du blar i hovedskjema   
\(db-update\). Foreløpig kan du ikke ha flere nivå.

```markup
<db-update  id="form" 
           key="bokid" 
        update="true"
        fields="bokid,tittel,pdato:date,isbn,antallsider:number" 
         table="bok"  >
    <span slot="heading">Rediger Bok</span>
</db-update>

<div class="table">
   <db-table connected="form:bokid" fields="eksemplarid,tillstand" 
             sql="select * from eksemplar">
       <span slot="caption">Eksemplar av valgt bok</span>
   </db-table>

   <db-table connected="form:bokid" fields="antall:number"
        sql="select count(u.utlaanid) as antall from 
            utlaan u join eksemplar e on (u.eksemplarid=e.eksemplarid)" >
        <span slot="caption">Antall utlån av denne boka</span>
   </db-table>
</div>
```

I eksemplet over vil de to tabellene følge valgt post i db-update. Dersom update="true" kan du redigere feltene og lagre nye verdier.   
key="nøkkel"  -- dette er nøkkelfelt i tabellen - antas å være auto-increment / serial primary key.  
                            dette feltet kan ikke redigeres \(disabled som default\).

![Redigering av bok, pilene blar gjennom hele datasettet](../../.gitbook/assets/dbupdate.png)

### Et eksempel på enkelt skjema

```markup
<head>
 <script src="/components/DbInsert.js"></script>
 <script src="/components/DbTable.js"></script>
</head>
<body>
    <div id="admin">
        <div class="table">
            <db-table id="table" update="true" delete="bok" 
              fields="bokid,tittel,fornavn,etternavn,antallsider:number"
              sql="select b.*,f.fornavn,f.etternavn from bok b 
                 join forfatter f on (b.forfatterid = f.forfatterid)" >
              <span slot="caption">Bøker</span>
            </db-table>
        </div>
        <db-insert id="form" fields="tittel,antallsider" 
                  foreign="forfatter.forfatterid:fornavn+etternavn" 
                  table="bok">
            <span slot="heading">Registrer Bok</span>
        </db-insert>
    </div>
</body>
```

