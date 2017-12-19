# Convention de nommage :
|Tag   |   |
|------|---|
|latest|Version de production (setté par défaut à la publication)|
|next  |Release Candidate (version de dev)|

# Commandes :
|Commande|   |
|--------|---|
|```npm login```|Se connecter|
|```npm publish```|Publie avec le tag 'latest' /!\ Penser à updater la version dans le package.json|
|```npm publish --tag <tag>```|Publie avec un tag différent de 'latest'|
|```npm unpublish <pkg>@<version>```|Supprimer une publication du repo|
|```npm dist-tag ls [<pkg>]```|Liste les tags|
|```npm dist-tag add <pkg>@<version> [<tag>]```|Changement du tag de la version publiée\
|```npm dist-tag rm <pkg> <tag>```|Effacer le tag du package|
|```npm view <pkg>```|Détails du package (liste de tous les publications effectuées, liste des publications actuellement en ligne, package.json)|

# Example :
```
npm publish 0.2.0-rc1
npm dist-tag add my-pkg@0.2.0-rc1 next
npm dist-tag add my-pkg@0.1.14 latest
npm unpublish my-pkg@0.1.10-rc1
   + my-pkg@0.1.15-rc2
npm view my-pkg
```
