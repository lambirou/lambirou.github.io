# Configuration

Alors que les conventions enlèvent le besoin de configurer tout CakePHP, vous
aurez tout de même besoin de configurer quelques options de configurations
comme les accès à la base de données.

De plus, certaines options de configuration facultatives vous permettent de
changer les valeurs par défaut & les implémentations avec des options qui
conviennent à votre application.

## Configurer votre Application

La configuration est généralement stockée soit dans les fichiers PHP ou INI, et
chargée pendant le bootstrap de l'application. CakePHP est fourni avec un
fichier de configuration par défaut, mais si cela et nécessaire, vous pouvez
ajouter des fichiers supplémentaires de configuration et les charger dans le
bootstrap de votre application. :php:class:`Cake\\Core\\Configure` est utilisée
pour la configuration globale, et les classes comme `Cache` fournissent les
méthodes `config()` pour faciliter la configuration et la rendre plus
transparente.

### Configuration Générale

Ci-dessous se trouve une description des variables et la façon dont elles
modifient votre application CakePHP.

**debug**
Change la sortie de debug de CakePHP. `false` = Mode Production. Pas de
messages, d'erreurs ou d'avertissements montrés. `true` = Errors et
avertissements montrés.

**App.namespace**
Le namespace sous lequel se trouvent les classes de l'app.

> Quand vous changez le namespace dans votre configuration, vous devez
> aussi mettre à jour le fichier **composer.json** pour utiliser aussi
> ce namespace. De plus, créer un nouvel autoloader en lançant
> `php composer.phar dumpautoload`.

.. \_core-configuration-baseurl:

**App.baseUrl**
Décommentez cette définition si vous **n'** envisagez **pas** d'utiliser le
mod_rewrite d'Apache avec CakePHP. N'oubliez pas aussi de retirer vos
fichiers .htaccess.

**App.base**
Le répertoire de base où l'app se trouve. Si à `false`, il sera détecté
automatiquement.

**App.encoding**
Définit l'encodage que votre application utilise. Cet encodage est utilisé
pour générer le charset dans le layout, et les entities encodés. Cela doit
correspondre aux valeurs d'encodage spécifiées pour votre base de données.

**App.webroot**
Le répertoire webroot.

**App.wwwRoot**
Le chemin vers webroot.

**App.fullBaseUrl**
Le nom de domaine complet (y compris le protocole) vers la racine de votre
application. Ceci est utilisé pour la génération d'URLS absolues. Par
défaut, cette valeur est générée en utilisant la variable d'environnement
\$\_SERVER. Cependant, vous devriez la définir manuellement pour optimiser la
performance ou si vous êtes inquiets sur le fait que des gens puissent
manipuler le header `Host`.
Dans un contexte de CLI (à partir des shells), `fullBaseUrl` ne peut pas
être lu dans \$\_SERVER, puisqu'il n'y a aucun serveur web impliqué. Vous
devez le spécifier vous-même si vous avez besoin de générer des URLs à
partir d'un shell (par exemple pour envoyer des emails).

**App.imageBaseUrl**
Le chemin Web vers le répertoire public des images dans webroot. Si vous
utilisez un :term:`CDN`, vous devez définir cette valeur vers la
localisation du CDN.

**App.cssBaseUrl**
Le chemin Web vers le répertoire public des css dans webroot. Si vous
utilisez un :term:`CDN`, vous devez définir cette valeur vers la
localisation du CDN.

**App.paths**
Les chemins de Configure pour les ressources non basées sur les classes.
Accepte les sous-clés `plugins`, `templates`, `locales`, qui
permettent la définition de chemins respectivement pour les plugins, les
templates de view et les fichiers de locales.

**App.jsBaseUrl**
Le chemin Web vers le répertoire public des js dans webroot. Si vous
utilisez un :term:`CDN`, vous devriez définir cette valeur vers la
localisation du CDN.

**Security.salt**<br>
Une chaîne au hasard utilisée dans les hashages. Cette valeur est aussi
utilisée comme sel HMAC quand on fait des chiffrements symétriques.

**Asset.timestamp**<br>
Ajoute un timestamp qui est le dernier temps modifié du fichier particulier
à la fin des URLs des fichiers d'asset (CSS, JavaScript, Image) lors de
l'utilisation des helpers adéquats.
Valeurs valides:
(bool) `false` Ne fait rien (par défaut)
(bool) `true` Ajoute le timestamp quand debug est à `true`
(string) 'force' Ajoute toujours le timestamp.

### Classe Config

`class` BabiPHP\Config\\**Config**

La nouvelle classe Configure de CakePHP peut être utilisée pour stocker et
récupérer des valeurs spécifiques d’exécution ou d’application. Attention,
cette classe vous permet de stocker tout dedans, puis de l’utiliser dans toute
autre partie de votre code: une tentative évidente de casser le modèle MVC avec
lequel CakePHP a été conçu. Le but principal de la classe Configure est de
garder les variables centralisées qui peuvent être partagées entre beaucoup
d’objets. Souvenez-vous d’essayer de suivre la règle “convention plutôt que
configuration” et vous ne casserez pas la structure MVC que nous avons mis en
place.

Vous pouvez accéder à `Config` partout dans votre application::

```php
    Config::get('debug');
```

#### Ecrire des Données de Configuration

`method` BabiPHP\Config\Config::**set($key, $value)**

Utilisez `set()` pour stocker les données de configuration de
l'application::

```php
    Config::set('Company.name','Pizza, Inc.');
    Config::set('Company.slogan','Pizza for your body and soul');
```

> La notation avec points utilisée dans le paramètre `$key` peut
> être utilisée pour organiser vos paramètres de configuration dans des
> groupes logiques.

L'exemple ci-dessus pourrait aussi être écrit en un appel unique::

```php
    Config::set('Company', [
        'name' => 'Pizza, Inc.',
        'slogan' => 'Pizza for your body and soul'
    ]);
```

Vous pouvez utiliser `Config::set('debug', $bool)` pour intervertir les
modes de debug et de production à la volée. C'est particulièrement pratique pour
les interactions JSON quand les informations de debug peuvent entraîner des
problèmes de parsing.

#### Lire les Données de Configuration

`method` BabiPHP\Config\Config::**get(\$key)**

Utilisée pour lire les données de configuration à partir de l'application. Par
défaut, la valeur de debug de CakePHP est au plus important. Si une clé est
fournie, la donnée est retournée. En utilisant nos exemples du write()
ci-dessus, nous pouvons lire cette donnée::

```php
    Configure::get('Company.name');    // Renvoie: 'Pizza, Inc.'
    Configure::get('Company.slogan');  // Renvoie: 'Pizza for your body and soul'

    Configure::get('Company');

    //yields:
    ['name' => 'Pizza, Inc.', 'slogan' => 'Pizza for your body and soul'];
```

Si \$key est laissée à null, toutes les valeurs dans Configure seront retournées.

#### Vérifier si les Données de Configuration sont Définies

`method` BabiPHP\Config\Config::**check(\$key)**

Utilisée pour vérifier si une clé/chemin existe et a une valeur non-null:

```php
    $exists = Config::exists('Company.name');
```
