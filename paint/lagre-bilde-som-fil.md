# Lagre bilde som fil

Vi har allerede et menyvalg for å lagre filen. Den kjører en funksjon i filen NewPage.js

{% tabs %}
{% tab title="saveToFile" %}
```javascript
function saveToFile() {
  const np = g("newpage");
  makeForm(np,"save-file", () => {}, () => {
    console.log("file saved");
  });
}
```
{% endtab %}

{% tab title="makeForm" %}
```javascript
function makeForm(np, id, actions, ok) {
  np.classList.remove("hidden");
  const template = /** @type {HTMLTemplateElement} */ (g(id));
  const clone = template.content.cloneNode(true);
  np.innerHTML = "";
  np.style = "";   // drop styles added by code
  np.append(clone);

  const btnOK = g("ok");
  btnOK.addEventListener("click", (e) => {
    np.classList.add("hidden");
    if (ok) ok();
  });

  const btnCancel = g("cancel");
  btnCancel.addEventListener("click", (e) => {
    np.classList.add("hidden");
  });

  if (actions) actions();
}
```
{% endtab %}
{% endtabs %}

Denne versjonen henter bare et template \("save-file"\) fra html og viser det som et skjema.  
I skjema kan du sette navn på filen og du har OK og Cancel.  
Vi skal skrive kode som kjøres ved klikk på OK.

Dersom du ser på koden for saveToFile ser du at den sender funksjonen under som parameter **ok**.  
`() => { console.log("file saved"); }` .  
Jeg har googla "_javascript save png to file_" og fant denne koden:

```text
<a href="#" class="button" 
id="btn-download" download="my-file-name.png">Download</a>

var button = document.getElementById('btn-download');
button.addEventListener('click', function (e) {
    var dataURL = canvas.toDataURL('image/png');
    button.href = dataURL;
});
```

### Dagens oppdrag \(it2\)

Bruk denne koden til å lagre tegninger som fil \(png\). 

* Du må endre template "save-file" i paint.html slik at "ok" knappen blir en `<a>` som vist.
* Event-lytteren settes opp automatisk for "ok" - du må bare sende en funksjon som skal kjøres.
* Du trenger bare skifte ut `console.log(..)` med den nye koden.
* Merk at **canvas** i eksemplet skal være en kobling til det canvas som skal lagres - må endres i din kode.
* Sørg også for at filnavnet brukeren velger blir satt som egenskapen **download** på "\#ok". Du trenger muligens setAttribute\( .. \) for å gjøre det.

