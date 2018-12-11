# String

## String-funksjoner

| Funksjon | Eksempel |
| :--- | :--- |
| s.length | "abc".length === 3 |
| s.includes | "ole petter".includes\("pe"\) === true |
| s.charAt | "abcde".charAt\(2\) === "c" |
| s.charCodeAt | "abcde".charCodeAt\(2\) === 99 |
| s.endsWith | "abcdef".endsWith\("def"\) === true |
| s.indexOf | "abcde".indexOf\("c"\) === 2    // -1 if not found |
| s.match | "abcdefgh".match\(/\[aeiouy\]/gi\) =&gt; \["a", "e"\] |
| s.padEnd | "1.0".padEnd\(6,"0"\) === "1.0000" |
| s.padStart | "1".padStart\(4,"0"\) === "0001" |
| s.repeat | "12".repeat\(4\) === "12121212" |
| s.replace | "søvnløs".replace\(/ø/g, "o"\) === "sovlos" |
|  | "søvnløs".replace\("ø", "o"\) === "sovnløs" |
| s.search | "og dermed".search\(/er/\) === 4  // -1 dersom ikke funnet |
| s.slice | "abcdefg".slice\(1\) === "bcdefg" |
|  | "abcdefg".slice\(2,4\) === "cd"  // slutter rett før pos 4 |
| s.split | "a b c d".split\(" "\) =&gt; \[ "a" , "b" , "c" \]  |
|  | "a b c d".split\(" ", 2\) =&gt; \[ "a" , "b" \]  |
| s.startsWith | "abcde".startsWith\("ab"\) === true |
| s.substr | "abcde".substr\(1\) === "bcde" |
|  | "abcde".substr\(-2\) === "de" |
|  | "abcdefghij".substr\(2,3\) === "cde" |
| s.toLowerCase | "ABC".toLowerCase\(\) === "abc" |
| s.toUpperCase | "abc".toUpperCase\(\) === "ABC" |
| s.trim | " abc ".trim\(\) === "abc" |
| s.trimStart | " abc ".trimStar\(\) === "abc " |
| s.trimEnd | " abc ".timEnd\(\) === " abc" |

