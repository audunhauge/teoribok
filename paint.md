# Paint - design av gui

Vi skal lage en simple paint versjon, du kan hente første versjon fra [https://github.com/audunhauge/jspaint/tree/v1.0](https://github.com/audunhauge/jspaint/tree/v1.0)

![](.gitbook/assets/paint.png)

På venstre side har vi verktøy - peker firkant polygon polyline og visk.  
Tegneområde \(canvas\) til høyre og fargevelgere nederst \(strek og fyll\).  
Oppgaven er å lage denne layouten med html + css. Alle verktøy er ren css, en div pr figur.  
Du finner en del hint under.

{% tabs %}
{% tab title="Firkant" %}
```css
/* Hopper over peker - den er litt komplisert.
   De som ikke er vist er rett fram (slik som sirkel - border-radius 50%)
   Eller kan lett utledes fra eksemplene.
   Peker ikke vist her.

Regelen for firkanten blir slik: */
#tools > div:nth-child(2) {
  border: solid brown 3px;
}

/*
For alle de andre bruker vi samme type selector: nth-child(x)
Du trenger bare bytte ut x med nr på den diven regelen skal styre
Prøv å lage løsning selv før du sjekker løsningsforslag
*/
```
{% endtab %}

{% tab title="Polygon" %}
```css
/* her bruker vi et triks - border rundt en firkant
   med 0 bredde og 0 høyde - alle sidene er transparent - bortsett 
   fra border-bottom - det er denne som blir trekanten
*/
  width: 0;
  height: 0;
  border-top: 0 solid transparent;
  border-left: 38px solid transparent;
  border-right: 38px solid transparent;
  border-bottom: 48px solid green;
```
{% endtab %}

{% tab title="Viskelær" %}
```css
/* bruker gradient til å få to farger i en div, kan ha så mange dul vil */
#tools > div:nth-child(6) {
  width: 64px;
  height: 34px;
  background: linear-gradient(to right, red 0%, red 49%, blue 50%, blue 100%);
  transform: rotate(-45deg);
  margin-top: 3rem;
  margin-bottom: 3rem;
}
```
{% endtab %}
{% endtabs %}

Sjekk ut html filen vist under. Som du ser så har vi en div med verktøy \(tools\), et canvas og fargevelger for outline og fill. I CSS er det vist litt styling for tools - spesielt den første div'en som skal være en peker.  
I JS er det vist to enkle classer \(dette er ikke pensum for it-1\). Du kan sjekke dem ut om du er interessert.

{% tabs %}
{% tab title="HTML" %}
{% code title="paint.html" %}
```javascript
 <div id="main">
        <div id="tools">
            <div title="pointer"></div>
            <div title="square"></div>
            <div title="circle"></div>
            <div title="polygon"></div>
            <div title="polyline"></div>
            <div title="eraser"></div>
        </div>
        <div id="draw">
            <canvas id="canvas" width="1024" height="800"></canvas>
        </div>
        <div id="colors">
            <div title="red"></div>
            <div title="green"></div>
            <div title="blue"></div>
            <div title="yellow"></div>
            <div title="black"></div>
        </div>
        <div id="fill">
            <div title="red"></div>
            <div title="green"></div>
            <div title="blue"></div>
            <div title="yellow"></div>
            <div title="black"></div>
        </div>
    </div>
```
{% endcode %}
{% endtab %}

{% tab title="CSS" %}
```css

#tools > div {
  width: 64px;
  height: 64px;
  border: solid black 1px;
  margin: 1rem;
}

#tools > div:nth-child(1) {
  position: relative;
  width: 0;
  height: 0;
  border-top: 0 solid transparent;
  border-left: 18px solid transparent;
  border-right: 18px solid transparent;
  border-bottom: 28px solid darkslategrey;
  transform: rotate(-45deg) translate(2px, -4px);
}

#tools > div:nth-child(1):after {
  content: "";
  width: 12px;
  height: 6px;
  background-color: darkslategrey;
  position: absolute;
  transform: rotate(-90deg) translate(-32px, -7px);
  border: solid black 1px;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
class Point {
    /**
     * Create a point given x,y
     * @param {{x:number,y:number}} point (x,y)
     */
  constructor({ x, y }) {
    this.x = x;
    this.y = y;
  }
}

/**
 * A square shape
 */
class Square extends Point {
    /**
     * 
     * @param {{x:number,y:number,w:number,h:number,c:string}} w=width,h=height
     */
  constructor({ x, y, w, h, c }) {
    super({ x, y });
    this.w = w;
    this.h = h;
    this.c = c;
  }
  /**
   * Draw the figure on given canvas
   * @param {CanvasRenderingContext2D} ctx canvas to draw on
   */
  render(ctx) {
    ctx.beginPath();
    ctx.strokeStyle = this.c;
    ctx.strokeRect(this.x, this.y, this.w, this.h);
  }
}
```
{% endtab %}
{% endtabs %}



