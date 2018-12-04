# Uke 45

## Binærtall

Vi lagde [denne](https://github.com/audunhauge/audunhauge.github.io/tree/master/it1/binaer) \(link til kode\) binærkalkulatoren. Du kan [teste](https://audunhauge.github.io/it1/binaer/bin.html) kalkulatoren.

Merk bruken av ::after slik at rutene får tallverdien plassert over \(rotert 45grader\).  
Merk også bruken av `content: attr(data-tall);` som henter en verdi fra html elementet.

{% code-tabs %}
{% code-tabs-item title="bin.css" %}
```css
div.bit:after {
    font-size: 0.8em;
    color: blue;
    position: absolute;
    content: attr(data-tall);
    top: -24px;
    left: 0;
    transform: rotate(-45deg);
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="bin.html" %}
```markup
    <div id="main">
        <div id="register">
            <div class="bit" data-tall="128" id="01"></div>
            <div class="bit" data-tall="64" id="02"></div>
            <div class="bit" data-tall="32" id="03"></div>
            <div class="bit" data-tall="16" id="04"></div>
            <div class="bit" data-tall="8" id="05"></div>
            <div class="bit" data-tall="4" id="06"></div>
            <div class="bit" data-tall="2" id="07"></div>
            <div class="bit" data-tall="1" id="08"></div>
        </div>
    </div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Datamaskiner bruker binærtall internt \(CPU bruker binærtall\)  
Et binærtall slik som 11011011 kan konverteres til desimal slik:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |

Summer 128+64+16+8+2+1 \(der hvor binærtallet har siffer 1\).

### Lekse

{% page-ref page="../teori/digital-samtid.md" %}



