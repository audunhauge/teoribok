---
description: Cascading style sheets
---

# CSS

## CSS-selectors

Når du skriver en css-regel bruker du en css-selector til å bestemme hvilket/hvilke elementer regelen skal gjelde for. 

### tag-selector

{% tabs %}
{% tab title="div.css" %}
```css
div {
  color: green;
}
```
{% endtab %}

{% tab title="span.css" %}
```css
span {
  background-color: rgb(12,123,205);
}
```
{% endtab %}
{% endtabs %}

Her gjelder regelen for alle &lt;div&gt; i dokumentet, de får grønn skriftfarrge. Dette er et eksempel på en **tag**- selector \(slik som **div span p article table td li ol ul** ...\)

