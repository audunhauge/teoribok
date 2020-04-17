# Farger og linjetykkelse

## Utvidelese av color-swatches \(fargekladder?\) \(it1\)

I versjon 1.1 - 1.8 har vi 5 farger å velge mellom for strek og fyll. Nå skal vi utvide slik at vi har en skala for hver hovedfarge. Her kan det være lurt å sjekk color.adobe.com for å se hvordan du kan sette sammen greie kombinasjoner. Vi tar det ikke helt dit, men ønsker følgende struktur:

* [ ]  5-6 fargegrupper \(hver er en skala med f.eks rødfarger\)
* [ ] En måte å styre alpha \(gjennomsiktighet\).
* [ ] Mulighet til å velge farge fra en input:color og dra den over på en gruppe

### Første versjon - rødskala

{% tabs %}
{% tab title="HTML" %}
```markup
<div id="colors">
    <div>
        <div title="#800000"></div>
        <div title="#bb2020"></div>
        <div title="#cc4040"></div>
        <div title="#dd8080"></div>
        <div title="#ffb0b0"></div>
    </div>
   .... flere slike ...
 </div>
```
{% endtab %}

{% tab title="CSS" %}
```css

#colors > div,
#fill > div {
  width: calc(33px * 5);
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}

#fill > div > div,
#colors > div > div {
  width: 32px;
  height: 32px;
  margin: 8px;
  background-color: gray;
}
```
{% endtab %}

{% tab title="JS" %}
```javascript
// Legg til denne koden i setup()
// den setter farge på en div ut fra verdien i title

// set up color-swatches
  document.querySelectorAll('#colors > div > div[title]').forEach(e => {
    // @ts-ignore
    /** @type {HTMLElement} */ (e).style.backgroundColor = e.title;
  })
```
{% endtab %}
{% endtabs %}

### Slitsomt å lage en skala for hånd \(it2\)

Anta at vi setter en fargekode på \#colors &gt; div \(første div inne i colors\). Vi ønsker kode som bruker denne fargen til å lage en skala slik vi ser for rødt. For å få dette til kan det være nyttig å skifte fra RGB til HSV fargerom \(en annen måte å angi farger på\)

```javascript
function rgb2hsv({ r = 0, g = 0, b = 0 }) {
  r = r / 255;
  g = g / 255;
  b = b / 255;
  const minRGB = Math.min(r, Math.min(g, b));
  const maxRGB = Math.max(r, Math.max(g, b));
  let h = 0,
    s = 0,
    v = maxRGB;
  if (minRGB !== maxRGB) {
    // Colors other than black-gray-white:
    const d = r == minRGB ? g - b : b == minRGB ? r - g : b - r;
    h = r === minRGB ? 3 : b === minRGB ? 1 : 5;
    h = 60 * (h - d / (maxRGB - minRGB));
    s = (maxRGB - minRGB) / maxRGB;
  }
  return { h, s, v };
}
```

