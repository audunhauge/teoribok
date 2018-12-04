# Uke 44

## Pensum til prøve

## Litt html

HTML-tagger

* div     en blokk-inndeling - hele bredden
* span   en tekst bit, vanligvis bare noen få ord
* header   topptekst/overskrifter/meny
* main    hoved-innhold
* footer   bunntekst/kontaktinfo
* article   en tekst om ett emne - tenk blogginnlegg
* ol   ordered list, lista er vanligvis nummerert
* li    et element i en liste
* ul   uordna liste, markert med punkt
* a    lager en hyperlink, kobling til et anna dokument/nettside      &lt;a href="nySide.html"&gt;Link til sida &lt;/a&gt;
* p    lager en paragraf / avsnitt
* br   lager linjeskift \(du får ikke den tomme linja som med p\)
* hr   lager en vanrett linje \(horizontal rule\)
* img   &lt;img src="katt.png"&gt;  setter inn et bilde
* video   &lt;video src="film.mp4"&gt;&lt;/video&gt;
* audio   &lt;audio src="lyd.mp3"&gt;&lt;/audio&gt; 

## Skjema

* button  husk bruk &lt;button type="button"&gt;Lagre&lt;/button&gt;
* input    &lt;input type="text"&gt;
* form    &lt;form&gt; ..... &lt;/form&gt;

## Tabell

* table    starter tabellen
* thead    overskrifter for kolonnene i tabellen
* tbody    selve innholdet i tabellen
* caption     tittel for hele tabellen
* tr    table row  - rader i tabellen
* td   celler i tabellen - som ruter i excel
* th   overskrift \(egentlig som td, men med feit skrift\)

```markup
<table>
  <thead>
     <caption> Land og befolkning </caption>
     <tr>
        <th>Land</th> <th>Befolkning</th>
     </tr>
  </thead>
  <tbody>
     <tr>
        <td>Norge</td>
        <td>5.2</td>
     </tr>
     <tr>
        <td>Sverige</td>
        <td>9.2</td>
     </tr>
  </tbody>
</table>
```

## CSS

Lag kobling fra html slik: &lt;link rel="stylesheet" href="test.css"&gt;

### Skriv regler

#### Regler for elementer med id

&lt;div id="main"&gt; .... &lt;/div&gt;

```css
#main {
   egenskap : verdi ;
}
```

#### Regler for element med klasse

&lt;div class="neato"&gt; ... &lt;/div&gt;

```css
.neato {
   ...
}
```

#### Liste med css - egenskaper

* color
* background-color
* background-image:  url\("katt.png"\)
*    plassering og størrelse av bkg-bilde
* position
*    left
*    bottom
*    top
*    right
* margin
* border
* padding
* border-radius
* grid

### Animation

animation: navn varighet\(s\) dealy\(s\) repeat fill-mode easing;

```css
   animation: gli 3s 0.5s infinite linear;
   /* denne animasjonen
       har navnet gli
       varer i 3s
       venter 0.5s før den starter
       gjentas i det uendelige
       har jevn fart
   */
   
   animation: sprett 2s ease-in-out forwards;
   /* denne animasjonen
       har navnet sprett
       varer i 2s
       gjentas 1 gang
       starter og slutter seint
       ender med å vise siste frame
   */
```

## Regler for databaser

* Alle tabeller skal ha et nøkkelfelt på formen **tabellnavnid** . Dersom tabellen har navnet **bok**, da har nøkkelfeltet navnet **bokid**.
* Nøkkelfeltet skal være av typen **int**.
* Alle felt må ha type - standard er int - denne må skiftes til char for tekstfelt.
* Lag koblinger mellom tabeller
* Konverter til SQL

