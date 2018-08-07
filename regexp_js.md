Fonctions Javascript associées :
--------------------------------
| Fonction  | Commentaire                                   | Exemple
|-----------|-----------------------------------------------|--------
| search()  | Retourne la position de la première occurrence trouvée, sinon **-1** est retourné
| match()   | Retourne un tableau contenant toutes les occurrences recherchées
| split()   | Découper une chaîne suivant des caractères    | ` split(/[,:;]/) `
| replace() | Effectue un rechercher/remplacer              | ` text.replace(/\[b\]([\s\S]*?)\[\/b\]/g, '<strong>$1</strong>'); `
| RegExp.test() | Retourne **true** si le test est réussi, **false** sinon
| RegExp.exec() | Renvoie un tableau dont le premier élément contient la portion de texte trouvée sinon renvoie **null**

Object RegExp :
---------------
```javascript
 var myRegex = /contenu_à_rechercher/;
 var myRegex = new RegExp("^contenu_à_rechercher$"+ variable, "i"); // permet d'inclure des variables dans la regex
 myRegex.test('Chaîne de caractères');
 /contenu_à_rechercher/.test('Chaîne de caractères');
```

Options :
---------
| Option| Commentaire
|-------|------------
| i     | Ignore la casse              | ` /contenu_à_rechercher/i `
| g     | Rechercher plusieurs fois

Metacaractères :
----------------
| Caractère | Commentaire                  | Exemple
|-----------|------------------------------|--------
| \|    | OU                           | ` /contenu1\|contenu2/ `
| ^     | Début de chaîne
| $     | Fin de chaîne                | ` /^Raclette savoyarde$/.test("Raclette savoyarde") = true `
| []    | Contient les caractères      | ` [abcd] [a-z] [A-Z0-9] /[a-zâäàéèùêëîïôöçñ]/i `
| [^]   | Ne contient PAS              | ` [^é] [^0-9] `
| .     | N'importe quel caractère, à l'exception des sauts de ligne \n
| ?     | Peut apparaître 0 ou 1 fois  | ` /raclett?e/ `
| +     | 1 ou plusieurs fois          | ` /raclet+e/ `
| \*    | 0, 1 ou plusieurs fois       | ` /raclet*e/ `
| +? *? | Mode non-greedy, s'arrête à la 1ère occurence trouvée et non plus la dernière
| {n}   | le caractère est répété n fois
| {n,m} | le caractère est répété de n à m fois
| {n,}  | le caractère est répété de n fois à l'infini
| \\    | Echapper un metacaractère
| ()    | Parenthèses capturantes      | ` RegExp.$1 à RegExp.$9 `
| (?:)  | Parenthèses non capturantes  | ` /(?:https\|http\|ftp\|steam):\/\// `

Types génériques :
------------------
| Type      | Commentaire
|-----------|------------
| \d    | Caractère décimal (un chiffre)
| \D    | Caractère qui n'est pas décimal (donc pas un chiffre)
| \t    | Trouve une tabulation (U+0009)
| \n    | Retour à la ligne (U+000A)
| \r    | Retour chariot (U+000D)
| \f    | Saut de page (U+000C)
| \s    | Caractère blanc (espace, tabulation, saut de ligne ou saut de page)
| \S    | Caractère qui n'est pas un caractère blanc
| \w    | Caractère de mot : n'importe quel caractère alphanumérique, accentué ou non, y compris le tiret bas
| \W    | Caractère qui n'est pas un caractère de mot

Assertions :
------------
| Assertion | Commentaire
|-----------|------------
| \b    | Trouve une limite de mot
| \B    | Ne trouve pas de limite de mot

Fonction de remplacement :
--------------------------
```javascript
function(str, p1, p2, p3 /* ... */, offset, s)
```
| Parametre  | Commentaire
|------------|------------
| str    | contient la portion de texte trouvée par la regex
| p*     | contiennent les portions capturées ($1, ..., $9)
| offset | opt - contient la position de la portion de texte trouvée
| s      | opt - contient la totalité de la chaîne

## Exemples :
```javascript
 var email = "contact@email.com";
 if ( /^[a-z0-9._-]+@[a-z0-9._-]+\.[a-z]{2,6}$/.test(email) )
    // Adresse e-mail valide
 else
    // Adresse e-mail invalide
```
```javascript
 const regex = /^[a-z0-9._-]+@[a-z0-9._-]+\.[a-z]{2,6}$/;
 regex.test('0611223344') // true
 regex.test('+33 611223344') // true
 regex.test('06.11.22.33.44') // true
 regex.test('333-222-4444') // true
```
