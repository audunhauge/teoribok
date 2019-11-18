# Befolkningspyramide

## JSON API - hent befolkningsdata

På [http://api.population.io/\#!/population/retrievePopulationTableAllAges](http://api.population.io/#!/population/retrievePopulationTableAllAges) kan du hente JSON data for en mengde land. Vi skal lage en app som lar deg velge land og år - deretter tegnes en befolkningspyramide med disse valgene.

Bruk komponenten vi lagde sist som lager en Homebar med passende overskrift.

Bruk metoden som er beskrevet i [Praktiske eksempler](praktiske-eksempler.md#lese-en-fil) til å lese data fra api-linken.

{% code title="Eksempel med data for brazil" %}
```javascript
[
  {
    "females": 1815690,
    "country": "Brazil",
    "age": 0,
    "males": 1871248,
    "year": 1980,
    "total": 3686938
  },
  {
    "females": 1752173,
    "country": "Brazil",
    "age": 1,
    "males": 1801249,
    "year": 1980,
    "total": 3553422
  },
  {
    "females": 1696386,
    "country": "Brazil",
    "age": 2,
    "males": 1739250,
    "year": 1980,
    "total": 3435636
  },
  {
    "females": 1647740,
    "country": "Brazil",
    "age": 3,
    "males": 1684691,
    "year": 1980,
    "total": 3332431
  },
]
```
{% endcode %}

Eksemplet med data fra Brazil viser formatet som er brukt. Du må skrive kode som behandler denne Arrayen og tegner søyler for hver årsgruppe.

Søylene skal stables slik at de yngste er nederst, menn til venstre og kvinner til høyre.

![UK 1950](../.gitbook/assets/image%20%282%29.png)

Lag en webkompononent som tegner et slikt diagram:

```text
<pop-pyr country="Norway" year="1950"></pop-pyr> 
```

Webkomponenten finner du som [pop-pyr](custom-web-components.md#en-befolkningspyramide) .  
Bruk denne i en løsning hvor du kan sammenligne tre forskjellige land.  
Slik komponenten er nå - så vises ikke skala \(max av antall menn\). Prøv å forbedre komponenten slik at en skala vises.

Du kan også bruke canvas eller svg til å tegne diagrammet \(utvidet oppgave\).

