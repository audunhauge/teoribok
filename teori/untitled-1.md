---
description: Cascading style sheets
---

# CSS

## CSS-selectors

Når du skriver en css-regel bruker du en css-selector til å bestemme hvilket/hvilke elementer regelen skal gjelde for. 

### tag-selector

{% code-tabs %}
{% code-tabs-item title="div.css" %}
```css
div {
  color: green;
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="span.css" %}
```css
span {
  background-color: rgb(12,123,205);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Her gjelder regelen for alle &lt;div&gt; i dokumentet, de får grønn skriftfarrge. Dette er et eksempel på en **tag**- selector \(slik som **div span p article table td li ol ul** ...\)

