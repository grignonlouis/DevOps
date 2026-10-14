# Cours de DevOps

Exercices du Cours 2 - Pipelining

>Déployer une pipeline dans votre repo Github permettant d'écrire Hello World.
>Ecrivez trois jobs différents dans votre pipeline pour écrire votre nom, prénom et email. N'écrivez pas en dur ces informations dans votre .yml, utilisez les variables d’environnements de votre repo prévues à cet effet.
>Ecrivez une pipeline faisant tourner un script Python affichant ”Commit success!” qui se lance à chaque commit de l’utilisateur.
>Créez trois branches Dev, Val, Prod. Créez une pipeline qui affiche le nom de la branche dans laquelle elle tourne.
>Créez une pipeline qui divise un nombre par 2 dans la Dev, puis si le résultat est pair divise ce nombre par 4 dans la Val, puis par 8 dans la Prod. Si un nombre est impair, la pipeline doit arrêter son execution.

Exercice avancé

>Créez une pipeline qui déploye une application Hello World sur Github Pages (Vous pouvez prendre un fichier html simple que vous stockez dans votre repo).
