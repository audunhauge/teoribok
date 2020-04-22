# En bedre select versjon

Bruker skal kunne velge shapes med peker - løsningen vi har nå er mildt sagt dårlig. Første versjon var at vi tegna en firkant og fant overlap mellom alle Shapes og denne firkanten \(Shape.overlap \).  
Dette virka fint for uroterte firkanter, ikke veldig bra for sirkler \(men som omtrent\).  
Problemet oppstår når vi tillater roterte firkanter \(og andre figurer\).

![Den bl&#xE5; firkanten er rotert - n&#xE5; er det overlap med den r&#xF8;de](../.gitbook/assets/overlap.png)

For å komme enkelt ut av denne knipa laga jeg en ny test som sjekker senter + radius for hver figur for overlap. Problemet er selvsagt at da får jeg overlap mellom den røde og begge de blå - radius er slik at hele firkanten er inni, senter midt i firkanten.

## Overlap mellom polygoner

Dette er da den mer generell metoden - gitt to polygon \(minst trekant\) - true/false dersom de overlapper.  
Jeg googla og fant følgende kode:

```javascript
function polygonPolygon(points1, points2)
{
    var a = points1
    var b = points2
    var polygons = [a, b]
    var minA, maxA, projected, minB, maxB, j
    for (var i = 0; i < polygons.length; i++)
    {
        var polygon = polygons[i]
        for (var i1 = 0; i1 < polygon.length; i1 += 2)
        {
            var i2 = (i1 + 2) % polygon.length
            var normal = { x: polygon[i2 + 1] - polygon[i1 + 1],
                           y: polygon[i1] - polygon[i2] }
            minA = maxA = null
            for (j = 0; j < a.length; j += 2)
            {
                projected = normal.x * a[j] + normal.y * a[j + 1]
                if (minA === null || projected < minA)
                {
                    minA = projected
                }
                if (maxA === null || projected > maxA)
                {
                    maxA = projected
                }
            }
            minB = maxB = null
            for (j = 0; j < b.length; j += 2)
            {
                projected = normal.x * b[j] + normal.y * b[j + 1]
                if (minB === null || projected < minB)
                {
                    minB = projected
                }
                if (maxB === null || projected > maxB)
                {
                    maxB = projected
                }
            }
            if (maxA < minB || maxB < minA)
            {
                return false
            }
        }
    }
    return true
}
```

Problemet er nå å ta denne i bruk.  
Prøv om dere kan bruke denne istedenfor overlap/touching.  
Løsning finner dere som v1.9 \(legges ut snart\)

