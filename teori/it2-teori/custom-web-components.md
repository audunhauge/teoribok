# Custom web components

### En homebar

Overskrift med Tittel, navn, meny og info

{% code title="Homebar.js" %}
```javascript
class HomeBar extends HTMLElement {
  constructor() {
    super();
    const heading = this.getAttribute("heading") || "Demo";
    const username = this.getAttribute("username") || "Ole";
    const info = this.getAttribute("info") || "4 ledige";
    const menu = this.getAttribute("menu") || "Home";
    this._root = this.attachShadow({ mode: "open" });
    this._root.innerHTML = `
      <div id="home">
        <div id="heading">${heading}</div>
        <div id="menu">${menu}</div>
        <div id="username">${username}</div>
        <div id="info">${info}</div>
      </div>
          <style>
            #home {
                display: grid;
                align-items: center;
                grid-template-columns: 1fr 2fr 3fr 1fr;
                height: 70px;
                background: rgba(32,166,231,.8) linear-gradient(180deg,#20a8e9,rgba(30,158,220,.5)) repeat-x;
                color: #fff;
                overflow:hidden;
            }

            #home > div {
                font-size: 1.2em;
                height: 32px;
                padding: 5px;
                text-align: center;
            }
            div#title {
                font-size: 1.5em;
                white-space: nowrap;
                margin-left: 2em;
            }
          </style>
        `;
  }
  static get observedAttributes() {
    return ["username","heading","menu","info"];
  }
  attributeChangedCallback(name, oldValue, newValue) {
    this._root.querySelector("#"+name).innerHTML = newValue;
  }
}
window.customElements.define("home-bar", HomeBar);
```
{% endcode %}

### Bruksmåte

Lag en mappe med navnet komponenter i prosjektet ditt, opprett filen over.  
Du inkluderer filen som et vanlig script i header på html-filen din.  
Du kan nå lage instanser på det nye html-elementet slik:

```text
<home-bar title="Netbutikk"></home-bar>
```

### En digital klokke

{% code title="DigitalTime.js" %}
```javascript
// @ts-check
class DigitalTime extends HTMLElement {
    constructor() {
      super();
      let now = new Date();
      let h = now.getHours();
      let m = now.getMinutes();
      let s = now.getSeconds();
      this._root = this.attachShadow({ mode: "open" });
      this._root.innerHTML = `
       <div id="clock">
         <span id="h">${h}:</span>
         <span id="m">${m}:</span>
         <span id="s">${s}</span>
       </div>
       <style>
       #clock {
         width: 60px;
         background-color: blue;
         color:white;
         margin: 0.5em;
         padding: 5px;
         border-radius: 3px;
       }
       </style>
       `;
       setInterval(()=>{
        let now = new Date();
        let h = String(now.getHours());
        let m = String(now.getMinutes());
        let s = String(now.getSeconds());
        this.setAttribute("h",h);
        this.setAttribute("m",m);
        this.setAttribute("s",s);
       }, 1000);
    }
    static get observedAttributes() {
      return ["h","m","s"];
    }
    attributeChangedCallback(name, oldValue, newValue) {
      this._root.querySelector("#"+name).innerHTML = newValue;
    }
  }
  window.customElements.define("digi-time", DigitalTime);
```
{% endcode %}

### En befolkningspyramide \(defunkt\)

{% hint style="danger" %}
Den api-en som brukes her er nå død - finner ingen andre som leverer bef.data
{% endhint %}

{% code title="Pyramide.js" %}
```javascript
// @ts-check
class Pyramide extends HTMLElement {
  constructor() {
    super();
    const country = this.getAttribute("country") || "Norway";
    const year = this.getAttribute("year") || "1950";
    const caption = this.getAttribute("caption") || `${country} ${year}`;
    const width = this.getAttribute("width") || "400";
    const size = Number(this.getAttribute("size")) || 3;
    const height = (size + 2) * 100;
    this._root = this.attachShadow({ mode: "open" });
    this.halfw = Number(width) / 2;
    this.data = {}; // store fetched data
    this.country = undefined;
    this.year = undefined;
    this._root.innerHTML = `
        <div id="home">
          <div id="pyramide"></div>
          <div id="caption">${caption}</div>
        </div>
            <style>
            .soyle {
                position: relative;
                height: ${size}px;;
                width: 10px;
                left: calc(${width}px / 2);
            }
            .soyle.females {
                background-color: red;
            } 
            .soyle.males {
                top: -2px;
                background-color: blue;
                margin-top: -1px;
                transform: rotate(180deg);
                transform-origin: left;
            }
            #pyramide {
                position: relative;
                width: ${width}px;
                height: ${height}px;
                border: solid 1px gray;
                background-color: var(--mainBg);
                padding: 2px;
            }
            #home {
                margin-top: 1em;
                width: ${+width+10}px;
            }
            #caption {
                text-align:center;
            }
            </style>
          `;
    //  this.hentDataOgTegn(country, year);
  }
  hentDataOgTegn(country = "Norway", year = "1950") {
    let url = `http://api.population.io:80/1.0/population/${year}/${country}`;
    fetch(url)
      .then(r => r.json())
      .then(data => {
        this.data = data;
        this.behandle(data);
      })
      .catch(e => console.log("Dette virka ikke."));
  }
  behandle(data) {
    let divPyr = this._root.querySelector("#pyramide");
    divPyr.innerHTML = "";
    // let max = Math.max(... data.map(e => e.males));
    let max = data.reduce((s, e) => Math.max(s, e.males), 0);
    for (let i = data.length - 1; i >= 0; i--) {
      let aardata = data[i];
      let f = (this.halfw * Number(aardata.females)) / max;
      let m = (this.halfw * Number(aardata.males)) / max;
      let divm = document.createElement("div");
      let divf = document.createElement("div");
      divm.className = "soyle males";
      divf.className = "soyle females";
      divf.style.width = f + "px";
      divm.style.width = m + "px";
      divPyr.appendChild(divf);
      divPyr.appendChild(divm);
    }
  }
  caption() {
    this._root.querySelector("#caption").innerHTML = `${this.country} ${this.year}`;
  }
  static get observedAttributes() {
    return ["country", "year"];
  }
  attributeChangedCallback(name, oldValue, newValue) {
    if (name === "country") {
      this.country = newValue;
      this.hentDataOgTegn(this.country, this.year);
    }
    if (name === "year") {
      this.year = newValue;
      this.hentDataOgTegn(this.country, this.year);
    }
    this.caption();
  }
}
window.customElements.define("pop-pyr", Pyramide);
```
{% endcode %}



