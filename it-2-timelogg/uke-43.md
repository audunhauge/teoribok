# Uke 43

## Installasjon og drift av en node-server

Vi laster ned nodejs for vårt operativsystem og installerer på maskinen \(installere for windows/mac/linux\).

Deretter lager vi en ny mappe **webserver** som vi åpner i VS-code.  
Vi lager en ny fil med navnet **app.js** og legger inn følgende innhold:

{% tabs %}
{% tab title="app.js" %}
```javascript
// @ts-check
const CONNECTSTRING = "postgres://audun:123@localhost/bibliotek";

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
  console.log(`Server started on port ${PORT}`);
});

async function runsql(res, obj) {
  let results;
  let sql = obj.sql;
  let data = obj.data;
  await db.many(
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

CONNECTSTRING er koblingen til postgres-databasen, den er satt sammen av  
brukernavn:passord:server:database. 

For at dette skal virke på hver vår database må vi redigere denne

* bytt ut audun med ditt brukernavn
* passord med passordet for din bruker \(i postgres\)
* localhost lar vi stå
* bibliotek er navnet på databasen vi kobler oss till \(skiftes etter behov\)

Vi må så tilpasse postgres slik at dette virker:

* start konsoll/terminal i postgres 
* skriv kommandoen `alter user dittBrukernavn with password '123';` slik at passordet blir '123'.
* skriv kommandoen `alter database bibliotek owner to dittbrukernavn;` slik at du eier denne.

Nå kan vi starte app.js som en server:

* Start en terminal/konsoll/powershell og bruk **cd** til å komme inn i mappa **webserver**.
* Skriv `node app.js` for å starte serveren.
* Nå får du sikkert en feilmelding om at **express** ikke er installert.
* Skriv `npm install -save express` for å installere.
* Test med `node app.js` og gjenta for andre ting som mangler.
*  -- typisk `npm install -save pg-promise` 
* Til slutt bør serveren starte og gir melding `Server started on port 3000`.

Du kan nå åpne en fane i nettleseren og skrive inn **http://localhost:3000** og se **{ msg: ok }**

### Åpne terminal på en bestemt mappe i osx

Du kan redigere systemvalg på mac slik at det blir enkelt å åpne en terminal i en mappe:

Velg **Systemvalg** - **Tastatur**, deretter **Snarveier** og **Tjenester**  
bla ned til du finner **Filer og mapper,** sett kryss på **Nytt Terminalvindu på mappe** .



