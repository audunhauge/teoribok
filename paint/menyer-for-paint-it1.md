# Menyer for Paint \(it1\)

Jeg har lagt til kode som aktiveres av menyvalget New. Foreløpig fjerner den bare alle Shapes fra lista og visker ut canvas. Det vi skal lage er et skjema hvor bruker velger layout for arket de skal tegne på.

![Eksemple p&#xE5; &quot;New File&quot; skjema](../.gitbook/assets/newfile.png)

Oppdraget denne gang er da å lage en div med layout slik at vi får omtrent dette skjemaet.  
Dette kan gjøres ved å legge til en div over main som i utgangspunktet er skjult.  
**Gi den nye div-en id="newpage".** Dette slikk at menykoden finner den.  
Position absolute slik at det ligger ca midt på skjermen.  
Units trenger vi ikke ta med nå - alle mål i px.

Det første elementet kan lages som en &lt;select&gt;  
Deretter &lt;input value="portrait" type="radio" name="orientation"&gt;  
Merk at for at radio må alle valg ha samme **name** for at de skal virke som en radio-group.  
Du må også lage en label som viser en tekst for radioknappen - knappen har ikke egen tekst.

{% tabs %}
{% tab title="PageSize" %}
```markup
<select>
  <option>A4</option>
  <option>A5</option>
</select>
```
{% endtab %}

{% tab title="Orientation" %}
```markup
<input type="radio" name="orientation" value="portrait">
```
{% endtab %}

{% tab title="Width & Height" %}
```markup
<input id="width" type="number">
```
{% endtab %}

{% tab title="Background" %}
```markup
<input type="color">
```
{% endtab %}
{% endtabs %}

Når du har fått skjema til å se ordentlig ut - skal du sette på en klasse **hidden** slik at skjema er skjult.  
Bruk `display:non;` for denne klassen.

Jeg legger til kode som tar vekk **hidden** fra \#**newpage** når bruker klikker på New i menyen.

