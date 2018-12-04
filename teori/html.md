# HTML

## Strukturen på en web-side

I vs-code kan du lage en ny webside ved å opprette en ny fil \(gi den navnet test.html\) og skrive ! i editoren. Ved trykk på enter vil du da få følgende struktur:

{% code-tabs %}
{% code-tabs-item title="test.html" %}
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



Legg merke til at alle tagger \(ord som står inne i &lt; &gt; \) har en start  og en slutt.

Du vil typisk endre på  Document slik at du får satt en riktig tittel for din webside.

Her skal du bytte tittel, endre Document til Min Side.Merk at alle ord som er inne i &lt;&gt; \(vinkelhaker\) er tagger, kommandoer som styrer strukturen på sida.

Du skal nå legge inn din egen tekst mellomogtaggene:

```markup
<h1>Hei - dette er sida mi </h1>
Litt tekst (skriv det du ønsker)
<br>
Mer tekst
på flere linjer - vises som en linje.
<p> Du kan bruke p for paragraf eller br for break for å 
få til avsnitt/linjeskift
</p>
Du kan også legge inn 
<hr>
for å få en linje som deler sida
```

### HTML tagger du skal kjenne

* h1 .. h6 --- gir overskrift, h1 størst, h6 minst 
* p --- gir en paragraf litt tekst 
* br --- bryter linja der den står 
* div --- lager en boks med innhold,  &lt;div&gt;mye innhold som tar full bredde &lt;/div&gt;
* span --- marker et område i en linje noen ord 
* a --- lager en hyperlink link &lt;a href="adresse"&gt;link&lt;/a &gt; 
* img - bilde ![](filnavn.png) &lt;img src="filename.png"&gt;
* table --- lager en tabell \(eget kap om dette form --- lager et skjema \(eget kap\)



