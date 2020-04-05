# Paint - "angre funksjon"

## Angre siste tegneoperasjon \(it2\)

Alle figurer/shapes har blitt pusha inn i arrayet drawings. Dersom vi ønsker å slette siste Shape - kan vi enkelt kjøre drawings.pop\(\) og så tegne alle figurer på nytt.  
Prøv å oversette fra pseudo-kode til javascript før du ser på løsningsforslag.

{% tabs %}
{% tab title="Pseudo" %}
```text
// pseudo code
// <- betyr: element i mengden
bruker klikker på angre knappen (viskelær?)
  visk ut canvas
  dersom drawings inneholder minst en figur
    pop siste element fra drawings
    gjenta for figur  <- alle figurer i drawings
      figur.render()
```
{% endtab %}

{% tab title="JS" %}
```javascript
// bruker klikker på angre knappen (viskelær?)
// linje 272 - case "erase"
ctx.clearRect(0, 0, 1024, 800);
gtx.clearRect(0, 0, 1024, 800);
if (drawings.length > 0) {
  drawings.pop();
  for (const shape of drawings) {
    shape.render(ctx);
  }
}

```
{% endtab %}
{% endtabs %}

I den forrige versjonen av **activateTool** ble AT tilbakestillt for alle verktøy - dette bør ikke gjøres for slette-knappen. Dermed kan du tegne firkanter - angre siste - og fortsette med samme verktøy.

Her ser vi en klar fordel ved bruk av Objekter - hvert enkelt object har sin egen kode - **render** - som gjennskaper akkurat dette objektet. Dermed kan vi iterere gjennom samlingen og få dem til å tegne seg selv.

## Slette hele arket - nytt ark/fil \(it2\)

Jeg legger til et nytt verktøy \(egentlig en meny\) øverst - samme teknikk som før, men fjerner input:radio da disse ikke skal settes som aktivt verktøy - bare utføre en enkelt handling.  
Endrer litt på css slik at jeg kan bruke tekst istedenfor utf-8 ikoner.  
Det nye menyvalget blir da File - New som sletter alle figurer og tilbakestiller hele tegningen.  
Mye likt erase, men setter drawings = \[ \] og tilbakestiller farger: blå strek og transp. fyll.

### Design av fil-meny \(it1\)

Utfør endringene i html og css slik at vi har et nytt verktøy øverst med teksten **File** og submeny **New**.  
Dersom du bruker en span inne i div'en for å sentrere teksten - så merk at det er elementet du klikker på som skal ha title="new". Det nye verktøy/subverktøy skal ikke ha input:radio.

{% tabs %}
{% tab title="Hint" %}
```text
Prøv selv før du sjekker løsningsforslag.

Jeg kopierte og redigerte peker-menyen, sletta input:radio
bytta ut utf-8 ikoner med File og New.
Observerte at 3rem ble veldig stort for File.
La til en span og skrev regel for denne.
La til en klasse icon for alle andre (de med utf-8 ikoner) 
og skrev regel for denne klassen (la 3rem inn her)
```
{% endtab %}

{% tab title="HTML" %}
```markup
<div>
    <label>
       <div><span>File</span></div>
          <div>
             <div>
               <label>
                  <div><span title="new">New</span></div>
               </label>
           </div>
       </div>
    </label>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```css
div.icon {
  font-size: 3rem;
}

#tools label > div:nth-of-type(1) span {
  display:inline-block;
  padding-top:16px;
}
```
{% endtab %}
{% endtabs %}

