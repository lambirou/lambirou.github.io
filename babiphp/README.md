## Qu'est-ce que BabiPHP?

BabiPHP est un Framework de développement d'applications - un <i>toolkit</i> (trousse à outils) - pour les personnes qui créent des sites Web en PHP. Accessible, mais puissant, fournissant des outils nécessaires aux applications grosses et robustes. Son objectif est de vous permettre de développer des projets beaucoup plus rapidement que lorsque vous écrivez un code à partir de zéro, en fournissant un ensemble de bibliothèques enrichis pour les tâches requises, ainsi qu'une interface simple et une structure logique pour accéder à ces bibliothèques. BabiPHP permet de vous concentrer de manière créative sur votre projet en minimisant la quantité de code nécessaire pour une tâche donnée.

<br>

## Exigences du serveur

* HTTP Server. Par exemple: Apache. mod_rewrite est préférable, mais en aucun cas nécessaire
* PHP 5.6.0 ou plus (y compris PHP 7.1.x, 7.2.x)
* extension PHP mbstring
* extension PHP intl

<br>

## Installation

#### Installer via Composer:

Imaginons que vous souhaitiez créer une nouvelle application BabiePHP dans le dossier `my_app_name`. Pour ceci vous pouvez lancer la commande suivante:

```
composer create-project --prefer-dist lambirou/babiphp my_app_name
```

Une fois que Composer finit le téléchargement du squelette de l’application et des librairies de BabiPHP, vous devriez avoir maintenant une application BabiPHP qui fonctionne, installée via Composer. Assurez-vous de garder les fichiers composer.json et composer.lock avec le reste de votre code source.

#### Configuration rapide:

<ol>
<li>Ouvrez le fichier <i>src/config/Config.php</i> avec un éditeur de texte et définissez votre configuration en suivant les instructions dans les lignes de commentaire qui précèdent.</li>
<li>Si vous avez l'intention d'utiliser un chiffrement ou de gérer des utilisateurs, définissez votre clé de cryptage en éditant le fichier <i>src/config/Security.php</i>.</li>
<li>Dans le cas où vous souhaitez utiliser une base de données, ouvrez le fichier <i>src/config/Database.php</i> avec un éditeur de texte et définissez les paramètres de votre base de données.</li>
</ol>

> Vous devriez être maintenant capable de vous rendre sur le lien votre application BabiPHP et voir la page d’accueil par défaut.

Pour une meilleure sécurité, le système et tous les dossiers de l'application doivent être placés au-dessus de la racine Web afin qu'ils ne soient pas directement accessibles via un navigateur. Par défaut, les fichiers <b>.htaccess</b> sont inclus dans chaque dossier pour empêcher l'accès direct, mais il est préférable de les supprimer de l'accès public entièrement au cas où la configuration du serveur Web changerait ou ne respecterait pas le <b>.htaccess</b>.

Une mesure supplémentaire à prendre dans les environnements de production est de désactiver les rapports d'erreur PHP et toute autre fonctionnalité de développement. Dans BabiPHP, cela peut se faire en suivant les configurations décrites sur la page de sécurité .

C'est tout!

> Si vous êtes nouveau sur BabiPHP, lisez la section Mise en route du Guide de l'utilisateur (situé dans le repertoire `docs/`) pour commencer à apprendre comment créer des applications PHP dynamiques.

<br>

## Mise en route de BabiPHP

Toute application logicielle nécessite des efforts d'apprentissage. Nous avons fait de notre mieux pour minimiser le processus en le rendant aussi agréable que possible.

BabiPHP est framework <i>ready-to-use</i> (prêt à l'emploi), l'étape majeure consiste donc à l'installer, alors lisez le sujet sur l'installation dans la section ci-dessus.

Ensuite, lisez chaque page des sujets généraux dans l'ordre. Chaque sujet s'appuie sur le précédent, et comprend des exemples de code que vous êtes encouragés à essayer.

Une fois que vous comprenez les bases, vous serez en mesure d'explorer les pages de référence de classe et de référence d'aide pour apprendre à utiliser les différentes bibliothèques.

<br>

## Journal des modifications et Nouvelles fonctionnalités

Vous pouvez trouver une liste de toutes les modifications pour chaque version dans le <a href="https://github.com/lambirou/babiphp/blob/master/docs/CHANGELOG.md">journal des modifications</a> du guide de l'utilisateur.

<br>

## Vulnérabilités de sécurité

Si vous découvrez une vulnérabilité de sécurité au sein de BabiPHP, veuillez envoyer un courrier électronique à Roland Edi à contact.lambirou@gmail.com. Toutes les vulnérabilités de sécurité seront traitées rapidement.

<br>

## License

Consultez le [Contrat de Licence](/license).

<br>

## Reconnaissance

L'équipe BabiPHP tient à remercier tous les contributeurs au projet et vous, l'utilisateur de BabiPHP.

<br>

## Télécharger

[ [Archive zip](https://github.com/lambirou/babiphp/archive/master.zip) ] -
[ [Archive tar.gz](https://github.com/lambirou/babiphp/archive/master.tar.gz) ]

<br>

<p align="center">
<i>BabiPHP : The Framework Made in Babi (Abidjan) !</i>
</p>
