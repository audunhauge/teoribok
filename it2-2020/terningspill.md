# Terningspill

Vi lager et terningspill

{% tabs %}
{% tab title="terning.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terninger</title>
    <link rel="stylesheet" href="terninger.css">
</head>
<body>
    <div id="forklaring">Dette er et spill</div>
    <div id="spill">     
    </div>
    <div id="knapper">
        <button id="roll">Roll</button>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="terning.css" %}
```css
#spill {
    position: absolute;
    top: 10px;
    left: 10px;
    width: 600px;
    height: 600px;
    border: green solid 1px;
}

#forklaring {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 10px;
    left: 650px;
}

#knapper {
    width: 200px;
    height: 200px;
    position: absolute;
    top: 220px;
    left: 650px;
    border: blue solid 1px;
}
```
{% endtab %}
{% endtabs %}



