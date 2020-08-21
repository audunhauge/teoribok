# Terningspill

## Vi lager et terningspill.

Første versjon ser du i kodevinduet under.  
Når du har installert git på maskinen din  - da kan du klone  
[https://github.com/audunhauge/it2-2020.git](https://github.com/audunhauge/it2-2020.git) .  
Kommandoen du skriver er da:  
`git clone` [`https://github.com/audunhauge/it2-2020.git`](https://github.com/audunhauge/it2-2020.git) ``  
og du får da en lokal kopi av alle eksempler fra undervisningen.

{% tabs %}
{% tab title="terning.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terninger</title>
    <link rel="stylesheet" href="terninger.css">
</head>
<body>
    <div id="forklaring">Dette er et spill</div>
    <div id="spill">     
    </div>
    <div id="knapper">
        <button id="roll">Roll</button>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="terning.css" %}
```css
#spill {
    position: absolute;
    top: 10px;
    left: 10px;
    width: 600px;
    height: 600px;
    border: green solid 1px;
}

#forklaring {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 10px;
    left: 650px;
}

#knapper {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 220px;
    left: 650px;
    border: blue solid 1px;
}
```
{% endtab %}

{% tab title="terning.js" %}
```javascript
// @ts-check

function setup() {
    let terning = 1;
    let btnRoll = document.getElementById("roll");
    let divSpill = document.getElementById("spill");

    btnRoll.addEventListener("click", rollDice);

    function rollDice() {
        terning = Math.trunc(Math.random() * 6) + 1;
        divSpill.innerHTML = String(terning);
    }
}

```
{% endtab %}
{% endtabs %}



