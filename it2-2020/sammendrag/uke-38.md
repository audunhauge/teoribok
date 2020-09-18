# Uke 38

Denne uka har vi laget funksjoner som går gjennom en tabell og utfører arbeid på hvert element.  
Typisk bruker vi en løkke med denne utformingen.  
`for (let i=0; i<tabell.length; i += 1) {   let verdi = tabell[i]; .... }`  
Denne løkka skal du kjenne igjen som en måte å iterere \(gå gjennom\) en tabell.

Du bør også kjenne en alternativ metode som gjør akkurat det samme:  
`for (let verdi of tabell) { .....}`  
Denne gjør akkurat det samme, men som du ser starter denne alltid på første element.  
Med `for (let i=1; ... )`  kan jeg hoppe over ett eller flere elementer i starten.

Vi har laga en enkel funksjon som summerer verdiene i en tabell og gir tilbake \(return\) summen.

{% tabs %}
{% tab title="Standard" %}
```javascript
// skriver summer med alternativ for-løkke
function summer(tabell) {
  let sum = 0;
  for (let verdi of tabell) {
    sum += verdi;
  }
  return sum;
}

```
{% endtab %}

{% tab title="Advanced learners" %}
```javascript
// kan også bruke to innebygde array funksjoner

// array.forEach
function summer(tabell) {
  let sum = 0;
  tabell.forEach( v =>  sum += v)
  return sum;
}  

// array.reduce
function summer(tabell) {
  return tabell.reduce( (s,v) => s+v, 0);
}
```
{% endtab %}
{% endtabs %}

Du skal kunne lage en funksjon som tar imot en array \(array parameter\) og beregner summen av tallene i denne tabellen.

Test deg selv på [array funksjoner](https://matte.oppgaver.net/quiz?qid=46364)

