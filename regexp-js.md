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
| \d    | Trouve un caractère décimal (un chiffre)
| \D    | Trouve un caractère qui n'est pas décimal (donc pas un chiffre)
| \s    | Trouve un caractère blanc
| \t    | Trouve un retour à la ligne = caractère blanc
| \n    | Trouve une tabulation = caractère blanc
| \S    | Trouve un caractère qui n'est pas un caractère blanc
| \w    | Trouve un caractère « de mot » : une lettre, accentuée ou non, ainsi que l'underscore
| \W    | Trouve un caractère qui n'est pas un caractère « de mot »

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

## Exemple :
```javascript
 var email = "contact@email.com";
 if ( /^[a-z0-9._-]+@[a-z0-9._-]+\.[a-z]{2,6}$/.test(email) )
    // Adresse e-mail valide
 else
    // Adresse e-mail invalide
```