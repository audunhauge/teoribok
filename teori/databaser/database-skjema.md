# Database skjema

## Installasjon av node og npm

Søk på _install nodejs mac_ og installer \([https://nodejs.org/en/download/](https://nodejs.org/en/download/)\).  
Etter installasjon kan du åpne et nytt kommandovindu og teste:

{% tabs %}
{% tab title="Node" %}
```text
:~ bruker$  node
Welcome to Node,js vxx.xxx
Type .help for more information
// trykk ctrl+d for å avslutte node
```
{% endtab %}

{% tab title="NPM" %}
```
:~ bruker$  npm
Usage: npm <command>
.....
npm@x.xx.x /usr/local...
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
  console.log(`Quiz server started on port ${PORT}`);
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

I visual studio code kan du nå åpne en terminal ved å trykke cmd+shift+p og skrive **integ temi** .  
Du får nå fram en terminal inne i vs-code som er åpna i samme mappe som vs-code viser i filvinduet.  
Du kan da lett bruke **cd bibliotek** etc for å komme inn i bibliotek-mappa.  
Skriv **ls** og du skal se filene _app.js, bib.sql og package.json_ .

Skriv **npm install** i terminalvinduet for å legge til nødvendige node filer til prosjektet.  
Nå kan du teste at serveren virker ved å skrive  
**node app.js**   
Du skal se  
**Quiz server started on port 3000**

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
Du finner komponentene i mappa [it1/SikkertBibliotek](https://github.com/audunhauge/audunhauge.github.io/tree/master/it1/SikkertBibliotek).

### **DbTable** 

Du trenger  &lt;script src="DbTable.js"&gt;&lt;/script&gt; i html-filen, kan legges i &lt;head&gt;

```javascript
<db-table>  update="bok" delete="bok"
            fields="bokid:hidden,tittel,antallsider:number"
               sql="select * from bok">
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



