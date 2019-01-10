# Praktiske eksempler



## Variabeldeklarasjoner

```text
let tall = 12;
let navn = "ole";
let elev = { fornavn:"ole", etternavn:"olsen" };
let ferdig = false;
let tabell = [ 1,2,3 ];
```

### Const <a id="const"></a>

```text
const BREDDE = 12;
const NAVN = "ole";
const ELEV = { fornavn:"ole", etternavn:"olsen" };
const FERDIG = false;
const TABELL = [ 1,2,3 ];
```

Merk at enkle const slik som BREDDE,NAVN,FERDIG ikke kan modifiseres.

* Denne koden er gyldig: ELEV.fornavn = "ole hetland" // eleven har fått ett nytt mellomnavn
* Denne er ugyldig: ELEV = { fornavn:"ole hetland, etternavn:"olsen" } // lager ny elev
* Denne koden er gyldig: TABELL.push\(4\); // endrer innholdet i TABELL
* Denne er ugyldig: TABELL = \[1,2,3,4\]; // Lager ny tabell

### Interaksjon med skjema/html <a id="interaksjon-med-skjemahtml"></a>

```text
// hent verdi fra tekstfelt
let inpNavn = document.getElementById("navn");
let navn = inpNavn.value;

// hent inn en tallverdi
let inpAlder = document.getElementById("alder");
let alder = inpNavn.valueAsNumber;

// vis tekst i en div
let divTekst = document.getElementById("tekst");
divTekst.innerHTML = " tekst som skal vises";

// funksjon aktivert av en knapp
let btnBeregn = document.getElementById("beregn");
btnBeregn.addEventListener("click", beregning);

function beregning(event) {
    // kode ...
    // typisk linjene over som henter data fra skjema/viser data
}
```

### Legge html elementer til en div <a id="legge-html-elementer-til-en-div"></a>

```text
let divMain = document.getElementById("main");
let btnKlikkMeg = document.createElement("button");
btnKlikkMeg.id = "klikkmeg";
btnKlikkMeg.innerHTML = "Klikk Meg";
btnKlikkMeg.addEventListener("click",duKlikkaMeg);
divMain.appendChild(btnKlikkMeg);
// du må også lage funksjonen duKlikkaMeg
```

### Beregninger <a id="beregninger"></a>

```text
let verdi = (12 + 3) / 4;
let vinkel = Math.asin(3/4);
let minst = Math.min(verdi, vinkel);
```

### Betingelser og valg <a id="betingelser-og-valg"></a>

**enkel if**

```text
// enkel if
if ( betingelse ) {
    // handling dersom sann
} else {
    // handling dersom usann
}
```

**if else if**

```text
if ( betingelse1 ) {
    // handling dersom betingelse1
} else if ( betingelse2 ) {
    // handling dersom betingelse2
}
// kan gjentas med så mange betingelser som nødvendig
```

### Løkker <a id="l&#xF8;kker"></a>

**for løkke**

```text
for (let i=0; i < 10; i++) {
    // kode som gjentas 10 ganger
}
```

**while løkke**

```text
let i = 0;
while (i<10) {
    // kode som gjentas 10 ganger
    i++;
}
```

**travasering av array**

```text
// vi antar at tabell er en array
let antall = tabell.length;
for (let i=0; i < antall; i++) {
    let verdi = tabell[i];
    // kode som gjør noe med hver verdi
}
```

En moderne variant \(es6\)

```text
// vi antar at tabell er en array
for (let verdi of tabell) {
    // kode som gjør noe med hver verdi
}
```

**finn minste / største verdi i en array**

```text
// vi antar at tabell er en array av tall
// f.eks tabell = [1,2,3-5,8,0,1222]
let minst = Math.min( ... tabell);
let storst = Math.max( ... tabell);
// ... er spread operatoren
```

## Lese en fil

NB! Denne metoden virker bare dersom du laster sida fra en webserver.

I eksemplene under antar vi at funksjonen **behandle** tar seg av bearbeiding av motatt data.

**bruk av fetch**

Koden under bruker fetch metoden som støttes av moderne nettlesere slik som Chrome og Firefox.

```text
let url = "elevliste.json";
fetch(url).then(r => r.json())
  .then(data => behandle(data))
  .catch(e => console.log("Dette virka ikke."))
```

**bruk av xhr**

Denne metoden virker i alle nettlesere, også de som er gått ut på dato.

```text
var url = "elevliste.json";
var xhr = new XMLHttpRequest();
xhr.open('GET', url);
xhr.responseType = 'json';

xhr.onload = function() {
  behandle(xhr.response);
};

xhr.onerror = function() {
  console.log("Dette gikk ikke bra.");
};

xhr.send();
```

