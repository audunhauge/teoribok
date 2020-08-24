# Terningspill

## Vi lager et terningspill.

Første versjon ser du i kodevinduet under.

På mandag 24.08 skal vi sjekke at alle har git og kan bruke det på sin maskin.  
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
    <title>Terningspill</title>
    <link rel="stylesheet" href="terninger.css">
    <script src="terninger.js"></script>
</head>
<body>
    <div id="spill">
        <div id="t1" class="terning"></div>
        <div id="t2" class="terning"></div>
        <div id="t3" class="terning"></div>
        <div id="t4" class="terning"></div>
        <div id="t5" class="terning"></div>
    </div>
    <div id="knapper">
        <button id="roll">Roll</button>
    </div>
    <div id="meldinger"></div>
    <script>
        setup();
    </script>
</body>
</html>
```
{% endtab %}

{% tab title="terning.css" %}
```css
#spill {
  position: absolute;
  left: 10px;
  top: 10px;
  width: 500px;
  height: 500px;
  border: solid red 1px;
}

#knapper {
    position: absolute;
    left: 650px;
    top: 250px;
    width: 200px;
    height: 200px;
    border: solid blue 1px;
}

#meldinger {
    position: absolute;
    left: 650px;
    top: 10px;
    width: 200px;
    height: 200px;
    border: solid green 1px;
}

.terning {
    width: 64px;
    height: 64px;
    border-radius: 9px;
    border: gray 2px solid;
    margin: 5px;
    /* 
       text-align 
       padding-top
    */

}
```
{% endtab %}

{% tab title="terning.js" %}
```javascript
// @ts-check

function setup() {
    let t1 = document.getElementById("t1");
    let t2 = document.getElementById("t2");
    let t3 = document.getElementById("t3");
    let t4 = document.getElementById("t4");
    let t5 = document.getElementById("t5");
    // let divKnapper = document.getElementById("knapper");
    // let divMeldinger = document.getElementById("meldinger");
    let btnRoll = document.getElementById("roll");

    btnRoll.addEventListener("click", rullTerning);

    function rullTerning() {
        let terning = Math.trunc(Math.random() * 6 + 1);
        t1.innerHTML = String(terning);

        terning = Math.trunc(Math.random() * 6 + 1);
        t2.innerHTML = String(terning);

        terning = Math.trunc(Math.random() * 6 + 1);
        t3.innerHTML = String(terning);

        terning = Math.trunc(Math.random() * 6 + 1);
        t4.innerHTML = String(terning);
        
        terning = Math.trunc(Math.random() * 6 + 1);
        t5.innerHTML = String(terning);
    }
}

```
{% endtab %}
{% endtabs %}



