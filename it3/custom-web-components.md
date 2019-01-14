# Custom web components

## En homebar

Overskrift med Tittel, navn, meny og info

{% code-tabs %}
{% code-tabs-item title="Homebar.js" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

### Bruksmåte

Lag en mappe med navnet komponenter i prosjektet ditt, opprett filen over.  
Du inkluderer filen som et vanlig script i header på html-filen din.  
Du kan nå lage instanser på det nye html-elementet slik:

```text
<home-bar title="Netbutikk"></home-bar>
```

### En digital klokke

{% code-tabs %}
{% code-tabs-item title="DigitalTime.js" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

