<img src="readme/img/simplon.jpg" width="400">

----------------------

# ARCHITECTURE MVC
Découper les différentes étapes d'une architecture MVC avec node et mongo

Ce chapitre s'inscrit dans le module **Node MVC**

1. [ ] [Node MVC étape 1](https://github.com/simplonco/node-mvc-mongodb-step1)
    
2. [x] [Node MVC étape 2](https://github.com/simplonco/node-mvc-mongodb-step2)
    
3. [ ] [Node MVC étape 3](https://github.com/simplonco/node-mvc-mongodb-step3)

Vous pouvez trouver ce module dans les parcours suivants :

+ Développeur Web Fullstack

------------

### LES MODELS DE LA DATABASE

Dans le cadre de notre exemple cette matière première se trouve dans des champs, fermes, etc...

Mais ce n’est pas le restaurateur qui va les chercher directement,
tout comme notre app ne va pas directement chercher dans les fichier .db.

Il va faire appel à un grossiste qui va les rendre facilement accessibles,
en les indexant, empaquetant, définissant leurs caractéristiques etc...
(Les failles logiques de cet exemple c’est que c’est aussi le client du restaurant qui va à priori remplir les champs/fermes de produits, et aussi que le restaurateur va voir son gorssite à chaque fois qu’on lui commande un plat, mais n’y prêtons pas attention...)

Notre app va avoir besoin d’une interface similaire.
Il va lui falloir un engin de BDD, pour accéder à la matière première, comme mongoDB ou SQLite3.
C’est aussi grâce à cet engin qu’on va définir sous quel format on veut créer ou récupérer nos données.
Nos models.

Le model c’est par exemple le schema chez mongoose, ou la requête SQL de création de table chez sqlite3.
Et toutes les méthodes annexes qui permettent de protéger ce format.

### LES CONTROLLERS DE L’API

La distinction la plus difficile à faire est celle entre un model et un controller.
Les controllers c’est un peu l’équipe de cuistots.
Il y en a un qui est spécialisé sur les plats, l’autre sur les entrées, le dernier sur les desserts.
Les séparer c’est bien pour l’organisation d’abord parce-qu’il ne vont pas forcément avoir besoin des mêmes outils.
Mais aussi pour éviter la création de bugs quand mon app grossit.
SI jamais un jour je veux rajouter/modifier une nouvelle recette de dessert à mon menu,
je n’ai pas besoin de changer l’espace de travail de toute l’équipe et je n’ai que le cuistot en charge des desserts à former.

>“Oui mais c’est pas comme ça dans mon app, j’ai un model users, et un controller users.
>En cuisine je vais pas avoir une matière première carotte et un cuistot carotte !”

En effet, mais les controllers ne sont pas toujours dédiés à un model.
Imaginons dans le cadre d’une market place, le model comments suivant :

```
{
    id : String,
    user_id : String,
    shop_id : String,
    text : String,
    title: String,
    stars: Number
}
```

Et un controller comments avec plusieurs methodes.
Dont une méthode comme create qui n’utilisera que le model comments par exemple. 

Maintenant on veut pouvoir cliquer sur un produit et afficher une interface avec tout les commentaires sur la boutique qui le vend.
On va à priori créer une route pour pour pouvoir récupérer toutes ces infos.
Et cette route va nous renvoyer vers une des méthodes de notre controlleur comments.

Cette méthode aura besoin :
- du model shops pour récupérer le nom et la photo de la boutique grace au product_id passé dans la requête.
- du model comments pour récupérer les détails de chaque commentaires.
- du model users pour récupérer les noms et photos des users de chaque commentaires.
C’est une recette qui demande beaucoup d’ingrédients.

Inversement un controller auth qui va gérer tout nos méthodes de login/token etc...n’a pas de model correspondant.

Un controller peut donc avoir besoin de plusieurs models, avoir un model correspondant, ou pas.
Maintenant qu’on peut intéragir avec notre database on peut directement faire nos views.