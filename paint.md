# Paint

Vi skal lage en simple paint versjon, du kan hente versjon fra [https://github.com/audunhauge/jspaint/tree/v1.0](https://github.com/audunhauge/jspaint/tree/v1.0)

Sjekk ut html filen vist under. Som du ser så har vi en div med verktøy \(tools\), et canvas og fargevelger for outline og fill. I CSS er det vist litt styling for tools - spesielt den første div'en som skal være en peker.  
I JS er det vist to enkle classer \(dette er ikke pensum for it-1\). Du kan sjekke dem ut om du er interessert.

{% tabs %}
{% tab title="JS" %}
```
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
```

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
{% endtabs %}

