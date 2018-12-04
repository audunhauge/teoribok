# Uke 34

### Tirsdag 20.8

Du må installere siste verson av Visual Studioc Code og oppdatere til siste versjon av Chrome.  
Lag en ny mappe for faget, i denne mappa lager du nye mapper for hvert prosjekt/eksempel.   
Lag en mappe med navnet skjema-eksempel.   
Åpne VSCode og velg Åpne Mappe, bla fram til den nye tomme mappa for eksemplet.   
Nå klikker du på ikonet for å lage en ny tom fil - gi den navnet skjema.html   
Vi lager følgende html ved å skrive ! og trykke enter \(emmet abbreviation\).

#### Resultat

{% code-tabs %}
{% code-tabs-item title="skjema.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

</body>
</html>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Så gjør vi følgende endringer:

* Skift title fra Document til Skjema 
* Legg til link:css og gi navnet skjema.css 
* Legg til script:src og gi navnet skjema.js 
* Legg til script \(ikke med src\) nederst før slutt på body 
* Lag filene skjema.css og skjema.js ved cmd+click på linken, + lag fil.

Vi redigerte innholdet av skjema.css slik at vi har innholdet som vist under.  
Vi redigerte filen skjema.js på samme måte. 

Nå skal filene se slik ut \(klikk på fanene for å velge fil\):

{% code-tabs %}
{% code-tabs-item title="skjema.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="skjema.css">
    <script src="skjema.js"></script>
    <title>Document</title>
</head>
<body>

    <script>
      setup();
    </script> 
</body>
</html>
```
{% endcode-tabs-item %}

{% code-tabs-item title="skjema.css" %}
```css
body { background-color: red; }
```
{% endcode-tabs-item %}

{% code-tabs-item title="skjema.js" %}
```javascript
function setup() {
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

