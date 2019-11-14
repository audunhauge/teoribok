# Uke 48

Vi laga en kalender i html/css og javascript.  
Oppgaven var å lage en kalender som kan vise 1, 3 eller 12 måneder \(select-knapp\).  
Kalenderen skal la oss skifte år/mnd, den skal markere fridager, den skal vise ukenr  
og navn på ukedager \(Ma Ti On To Fr Lø Sø\).

Oppgaven er ganske kompleks - derfor prøver vi å bryte den ned i enkle trinn som kan mestres.

Første trinn var å få fram årstallet på skjermen med to knapper slik at vi kan bla fram og tilbake.  
Ved klikk på knappene skal årstallet endre seg.

{% tabs %}
{% tab title="cal.js" %}
```javascript
function setup() {
  let divYear = document.getElementById("year");
  let btnNext =  document.getElementById("nexty");
  let btnPrev = document.getElementById("prevy");
  
  btnPrev.addEventListener("click", prevY);
  btnNext.addEventListener("click", nextY);

  let year;
  let month;
  let day;
  
  function start() {
    year = 2018;
    month = 11;
    day = 28;
  }
  
  function show() {
    divYear.innerHTML = String(year);
  }
  
  function nextY(e) {
    year++;
    show();
  }
  
  function prevY(e) {
    year--;
    show();
  }
}   // slutt på setup
```
{% endtab %}
{% endtabs %}

Neste trinn var å gjøre det samme for måned, merk at når vi blar fra mnd=12 til neste, så må mnd bli 1 og året må økes med 1. Tilsvarende når vi blar bakover fra januar.  
Igjen lager vi en enkel løsning først som bare vise nr for måned

```javascript
// knapper for å bla mellom månder som for år
function show() {
  divYear.innerHTML = String(year);
  divMonth.innerHTML = String(month);
}

// versjon 1.
function nextM() {
  month++;
  show();
}  

// versjon 2.
function nextM() {
  if (month === 12) {
    month = 0;  // blir til 1 pga month++ senere
    year++;
  }
  month++;
  show();
}  
```

For å fikse visning av navn på måneder legger vi til følgende [Map](../it3/map-og-set.md#map):

```javascript
let monthNames = new Map();
// monthNames Mapper(konverterer) fra tall til tekst
// 1 ==> januar, 2 ==> februar ....
monthNames.set(1,"Januar");
...
monthNames.set(12,"Desember");

// ny versjon av show
function show() {
  divYear.innerHTML = String(year);
  divMonth.innerHTML = monthNames.get(month);
}
```

