# Linjetykkelse og overskrift \(it1\)

Linjetykkelse skal kunne velges - en mulighet er å vise en del forskjellige linjetykkelser og la bruker klikke på en for å sette linjetykkelse. Denne er jo litt begrensa, men kan duge som en start.

Lag en div som plasseres under pointers - skal inneholde linjer - 6 stykk.  
Linjer fra 1px -- 30px.

{% tabs %}
{% tab title="HTML" %}
```markup
<div id="linesize">
  div*6
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
#linesize {
}
```
{% endtab %}
{% endtabs %}

## Overskrift for programmet

Vi stjeler litt plass på toppen og legger inn en home-bar. Dette er for å lage en fin overskrift og for å ha en plass for standard meny-valg slik som New Save Load.

Koden for home-bar kan dere hente fra min github [https://github.com/audunhauge/db-components/blob/master/public/components/Homebar.js](https://github.com/audunhauge/db-components/blob/master/public/components/Homebar.js)

Eller bare kopiere herfra:

{% tabs %}
{% tab title="HomeBar.js" %}
```javascript
 
// @ts-check
class HomeBar extends HTMLElement {
  constructor() {
    super();
    const heading = this.getAttribute("heading") || "";
    const crumb = this.getAttribute("crumb") || "";
    const username = this.getAttribute("username") || "";
    this._info = {};
    let now = new Date();
    let datestr = now.toDateString();
    this._root = this.attachShadow({ mode: "open" });
    this._root.innerHTML = `
      <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
      <div id="home">
        <div id="menu" tabindex="0">
            <i class="material-icons">menu</i>
            <ul>
              <li data-link="/index">Home</li>
              <slot><li>simple menu</li></slot>
            </ul>
        </div>
        <div id="heading">${heading}</div>
        <div id="crumb">${crumb}</div>
        <div id="username">${username}</div>
        <div id="info">${datestr}</div>
      </div>
          <style>
            #home {
                display: grid;
                align-items: center;
                grid-template-columns: 1fr 1fr 2fr 3fr 1fr;
                height: 70px;
                background-color: rgba(32,166,231,.8);
                background-image: var(--grad, linear-gradient(180deg,#20a8e9,rgba(30,158,220,.5)) );
                color: #fff;
            }
            div#menu {
              place-self:center left;
              width: 180px;
            }
            div#menu ul,
            div#info > ul {
              text-align: left;
              text-transform: capitalize;
              visibility: hidden;
              list-style: none;
              margin: 0;
              padding: 5px;
              z-index:100;
              position: relative;
              top:-0px;
              color: black;
              background-color: rgb(245, 245, 245);
              box-shadow: 2px 2px 2px gray;
              border: solid gray 1px;
              border-radius: 4px;
              padding: 5px;
            }
            div#menu:focus-within ul,
            div#menu:hover ul,
            div#info:hover > ul {
               visibility: visible;
            }
            ::slotted(li:focus),
            ::slotted(li:hover),
            div#menu slot:hover,
            div#menu ul li:hover,
            div#info > ul > li:hover {
              background: rgb(32,166,231);
            }
            div#info li, div#menu li {
              padding: 2px;
            }
            #home > div {
                font-size: 1.2em;
                height: 32px;
                padding: 5px;
                text-align: center;
                white-space: nowrap;
            }
            div#heading {
                font-size: 1.5em;
                white-space: nowrap;
                margin-left: 2em;
            }
            #home i.material-icons {
              font-size: 32px;
            }
            @media not (screen and (-webkit-device-pixel-ratio: 1)) {
              #username , #info, #crumb { display:none; }
              #home {grid-template-columns: 1fr 1fr 3fr;}
            }
            @media screen and (max-width: 750px) {
              #username , #info { display:none; }
              #home {grid-template-columns: 1fr  1fr 3fr;}
            }
            @media screen and (max-width: 550px) {
              #username , #info, #crumb { display:none; }
              #home {grid-template-columns: 1fr 2fr; }
            }
          </style>
        `;

    this._root
      .querySelector("#crumb")
      .addEventListener("click", () => this.dispatchEvent(new Event("crumb")));
    this._root.querySelector("#menu").addEventListener("click", e => {
      let t = e.target;
      this._info.target = t;
      if (t.localName === "li" && t.dataset.link) {
        let link = t.dataset.link;
        location.href = `${link}.html`;
      } else this.dispatchEvent(new Event("menu"));
    });
    this._root.querySelector("#info").addEventListener("click", e => {
      let t = e.target;
      this._info.target = t;
      this.dispatchEvent(new Event("info"));
    });
    this._root
      .querySelector("#username")
      .addEventListener("click", () =>
        this.dispatchEvent(new Event("username"))
      );
  }

  get info() {
    return this._info;
  }

  static get observedAttributes() {
    return ["username", "heading", "menu", "info", "crumb", "getlinks"];
  }

  attributeChangedCallback(name, oldValue, newValue) {
    if (name === "username") {
      fetch(newValue)
        .then(r => r.json())
        .then(({ username }) => {
          this._root.querySelector("#username").innerHTML = username;
        })
        .catch(e => console.log("Dette virka ikke."));
        return;
    } 
    this._root.querySelector("#" + name).innerHTML = newValue;
    
  }
}

window.customElements.define("home-bar", HomeBar);
```
{% endtab %}

{% tab title="Bruk i html" %}
```markup
 // husk link i head
 <script src="Homebar.js"></script>
 
 <home-bar heading="Painter" >
        <li>New</li>
 </home-bar>
```
{% endtab %}
{% endtabs %}

Oppdraget i dag er å legge til home-bar og tilpasse slik at det ser ut som en naturlig del av programmet.  
Det er rimelig at en god del endringer må gjøres i CSS.

