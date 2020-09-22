# Første versjon - kart.

Vi lager en html-side og litt css slik at vi kan tegne et enkelt brukergrensesnitt.

{% tabs %}
{% tab title="rouge.html" %}
```markup
<body>
    <div id="main">
        <div id="board">
          (div*12)*12
        </div>
        <div id="info"></div>
        <div id="minimap"></div>
        <div id="status"></div>
    </div>
    <script>
        setup();
    </script>
</body>
```
{% endtab %}

{% tab title="rouge.css" %}
```css
:root {
    --board:calc(12*32px);
}

#main {
    position: relative;
    width:600px;
    height: 500px;
    margin:20px;
}
#main > div {
    border: solid gray 1px;
}

#board {
    position: absolute;
    left: 0;
    top: 0;
    width:var(--board);
    height: var(--board);
    display: grid;
    grid-template-columns: repeat(12,1fr);
}
#board > div {
    width:32px;
    height:32px;
    background-image: url("images/tiles32.png");
    background-position-x: 0px;
    background-position-y: 0px;
}

#info {
    position: absolute;
    right: 10px;
    top: 0;
    width:150px;
    height: 350px;
}
#minimap {
    position: absolute;
    right: 10px;
    bottom: 10px;
    width:120px;
    height: 120px;
}
#status {
    position: absolute;
    left: 0;
    bottom: 10px;
    width:var(--board);
    height: 100px;
}
```
{% endtab %}
{% endtabs %}

Innholdet i \#board er 12x12 ruter \(divs\). Disse settes til 32x32 px i css.  
Bakgrunnen i hver rute er henta fra tiles32.png  \(stjålet fra tyrant\). Dette er en samling med 32x32 bakgrunner som representerer terreng/gras/fjell osv.

