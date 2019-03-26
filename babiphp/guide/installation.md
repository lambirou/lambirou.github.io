# Installation

BabiPHP est rapide et facile à installer. Les conditions minimales requises sont un serveur web et une copie de BabiPHP, c’est tout! Bien que ce manuel se focalise principalement sur la configuration avec Apache (parceque c’est la plus simple à installer et configurer), BabiPHP fonctionnera sur une diversité de serveurs web tels que nginx, LightHTTPD ou Microsoft IIS.

## Exigences

- Un serveur HTTP. Par exemple: Apache. mod_rewrite est préférable, mais en
  aucun cas nécessaire.
- PHP 7.1.2 ou plus (y compris 7.2.x)
- L'extension PHP mbstring
- L'extension PHP intl
- L'extension PHP simplexml

> Avec XAMPP et WAMP, l'extension mbstring fonctionne par défaut.
> Dans XAMPP, l'extension intl est incluse mais vous devez décommenter
> `extension=php_intl.dll` dans **php.ini** et redémarrer le serveur dans
> le Panneau de Contrôle de XAMPP.
> Dans WAMP, l'extension intl est "activée" par défaut mais ne fonctionne pas.
> Pour la rendre fonctionnelle, dirigez-vous dans le dossier php (par défaut)
> **C:\\wamp\\bin\\php\\php{version}**, copiez tous les fichiers qui
> ressemblent à **icu\*.dll** et collez-les dans le répertoire bin d'apache
> **C:\\wamp\\bin\\apache\\apache{version}\\bin**. Ensuite redémarrez tous les
> services et tout devrait être bon.

Techniquement, un moteur de base de données n'est pas nécessaire, mais nous
imaginons que la plupart des applications vont en utiliser un. BabiPHP
supporte une diversité de moteurs de stockage de données :

- MySQL (5.5.3 ou supérieur)
- MariaDB (5.5 ou supérieur)
- PostgreSQL
- Microsoft SQL Server (2008 ou supérieur)
- SQLite 3

> Tous les drivers intégrés requièrent PDO. Vous devez vous assurer que vous
> avez les bonnes extensions PDO installées.

## Installer BabiPHP

Avant de commencer, vous devez vous assurer que votre version de PHP est à jour :

```sh
    php -v
```

Vous devez avoir PHP |minphpversion| (CLI) ou supérieur. Le serveur web doit
utiliser la même version de PHP que votre interface en ligne de commande.

## Installer Composer

BabiPHP utilise [Composer](http://getcomposer.org), un outil de gestion de
dépendances comme méthode officielle supportée pour l'installation.

- Installer Composer sur Linux et macOS

  1. Exécutez le script d'installation comme décrit dans la
     `documentation officielle de [Composer](http://getcomposer.org)
     et suivez les instructions pour installer Composer.
  2. Exécutez la commande suivante pour déplacer composer.phar vers un
     répertoire qui est dans votre path :

```sh
    mv composer.phar /usr/local/bin/composer
```

- Installer Composer sur Windows

  Pour les systèmes Windows, vous pouvez télécharger l'installeur Windows de
  Composer [ici](https://github.com/composer/windows-setup/releases/).
  D'autres instructions pour l'installeur Windows de Composer se trouvent dans
  le README [ici](https://github.com/composer/windows-setup).

## Créer un Projet BabiPHP

Maintenant que vous avez téléchargé et installé Composer, imaginons que vous
souhaitiez créer une nouvelle application BabiPHP dans le dossier my_app_name.
Pour ceci vous pouvez lancer la commande suivante :

```sh
    php composer.phar create-project --prefer-dist lambirou/babiphp my_app_name
```

Ou si Composer est installé globalement :

```sh
    composer self-update && composer create-project --prefer-dist lambirou/babiphp my_app_name
```

Une fois que Composer finit le téléchargement du squelette de l'application et
du cœur de la librairie de BabiPHP, vous devriez avoir une application BabiPHP
fonctionnelle, installée via Composer. Assurez-vous de garder les fichiers
composer.json et composer.lock avec le reste de votre code source.

Vous pouvez maintenant naviguer vers le chemin où vous avez installé
votre application BabiPHP et voir la page d'accueil par défaut. Pour changer
le contenu de cette page, modifiez: **src/resources/views/index.tpl**.

Bien que Composer soit la méthode d'installation recommandée, il existe des
versions pré-installées disponibles sur [Github](https://github.com/BabiPHP/BabiPHP/tags).
Ces téléchargements contiennent le squelette d'une application avec toutes
les dépendances installées.
Le `composer.phar` est aussi inclus donc vous avez tout ce qui est nécessaire
pour pouvoir l'utiliser.

## Réécriture d'URL

### Apache

Bien que BabiPHP soit conçu pour fonctionner avec mod_rewrite, et c'est
généralement le cas, nous avons remarqué que quelques utilisateurs ont du
mal à faire en sorte que tout se passe bien sur leurs systèmes.

Voici quelques choses que vous pourriez essayer pour que cela
fonctionne correctement. Premièrement, regardez votre fichier
httpd.conf (assurez-vous que vous avez édité le httpd.conf du système
plutôt que celui d'un utilisateur ou d'un site spécifique).

Ces fichiers peuvent varier selon les différentes distributions et les versions
d'Apache. Vous pouvez consulter
http://wiki.apache.org/httpd/DistrosDefaultLayout pour plus d'informations.

1. Assurez-vous que l'utilisation des fichiers `.htaccess` est permise et que
   AllowOverride est défini à All pour le bon DocumentRoot. Vous devriez voir
   quelque chose comme :

```apacheconf
    # Chaque répertoire auquel Apache a accès peut être configuré en
    # fonction des services et fonctionnalités autorisés et/ou
    # désactivés dans ce répertoire (et ses sous-répertoires).
    #
    # Tout d'abord, nous configurons le "défaut" pour qu'il s'agisse
    # d'un ensemble très restrictif de fonctionnalités.
    #
    <Directory />
        Options FollowSymLinks
        AllowOverride All
    #    Order deny,allow
    #    Deny from all
    </Directory>
```

2. Assurez-vous que vous avez chargé correctement mod_rewrite. Vous devriez voir quelque chose comme :

```apacheconf
    LoadModule rewrite_module libexec/apache2/mod_rewrite.so
```

Dans de nombreux systèmes, ces lignes seront commentées par défaut, vous
devrez donc simplement supprimer le symbole # en début de ligne.

Après avoir effectué les changements, redémarrez Apache pour être sûr
que les paramètres soient effectifs.

Vérifiez que vos fichiers `.htaccess` sont effectivement dans le bon
répertoire.

Vérifiez que vos fichiers `.htaccess` sont bien dans les bons répertoires.
Certains systèmes d'exploitation traitent les fichiers qui commencent par
**'.'** comme cachés et ne les copient donc pas.

3. Assurez-vous que votre copie de BabiPHP provient de la section
   téléchargements du site ou de notre dépôt Git, et qu'elle a été
   décompressée correctement, en vérifiant les fichiers `.htaccess`.

Le répertoire de BabiPHP (sera copié dans le répertoire supérieur de
votre application par bake) :

```apacheconf
       <IfModule mod_rewrite.c>
          RewriteEngine on
          RewriteRule    ^$    public/    [L]
          RewriteRule    (.*) public/$1    [L]
       </IfModule>
```

Le répertoire `public` de BabiPHP (sera copié dans la racine web de votre
application par bake) :

```apacheconf
       <IfModule mod_rewrite.c>
           RewriteEngine On
           RewriteCond %{REQUEST_FILENAME} !-f
           RewriteRule ^ index.php [QSA,L]
       </IfModule>
```

Si votre site BabiPHP a toujours des problèmes avec mod_rewrite,
vous pouvez essayer de modifier les paramètres des Hôtes Virtuels. Sur
Ubuntu, éditez le fichier **/etc/apache2/sites-available/default**
(l'endroit dépend de la distribution). Dans ce fichier, assurez-vous
que `AllowOverride None` a été changé en `AllowOverride All`,
donc vous avez :

```apacheconf
    <Directory />
        Options FollowSymLinks
        AllowOverride All
    </Directory>
    <Directory /var/www>
        Options FollowSymLinks
        AllowOverride All
        Order Allow,Deny
        Allow from all
    </Directory>
```

Sur macOS, une autre solution est d'utiliser l'outil [virtualhostx](http://clickontyler.com/virtualhostx/) pour créer un Hôte
Virtuel pour pointer vers votre dossier.

Pour de nombreux services d'hébergement (GoDaddy, 1and1), votre serveur web
est distribué à partir d'un répertoire utilisateur qui utilise déjà
mod_rewrite. Si vous installez BabiPHP dans un répertoire
utilisateur **http://exemple.com/~username/babiphp/**, ou toute autre
structure URL qui utilise déjà mod_rewrite, vous aurez devrez ajouter
des instructions RewriteBase aux fichiers `.htaccess` que BabiPHP
utilise (`.htaccess`, `public/.htaccess`).

Ceci peut être ajouté dans la même section que la directive RewriteEngine,
par exemple, votre fichier `.htaccess` dans `public` ressemblerait à :

```apacheconf
       <IfModule mod_rewrite.c>
           RewriteEngine On
           RewriteBase /path/to/app
           RewriteCond %{REQUEST_FILENAME} !-f
           RewriteRule ^ index.php [L]
       </IfModule>
```

Les détails de ces changements dépendront de votre configuration, et
peuvent inclure des choses supplémentaires qui ne sont pas liées à
BabiPHP. Veuillez vous référer sur la documentation en ligne d'Apache
pour plus d'informations.

4. (Facultatif) Pour améliorer la configuration de production, vous devez
   empêcher les ressources invalides d'être analysées par BabiPHP. Modifiez
   votre .htaccess dans `public` pour quelque chose comme :

```apacheconf
    <IfModule mod_rewrite.c>
        RewriteEngine On
        RewriteBase /path/to/app
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteCond %{REQUEST_URI} !^/(public/)?(img|css|js)/(.*)$
        RewriteRule ^ index.php [L]
    </IfModule>
```

Ce qui précède empêchera l'envoi de ressources incorrectes à index.php
et affichera à la place la page 404 de votre serveur web.

De plus, vous pouvez créer une page HTML 404 correspondante, ou utiliser la
page 404 de BabiPHP intégrée en ajoutant une directive `ErrorDocument` :

```apacheconf
    ErrorDocument 404 /404-not-found
```

### nginx

nginx n'utilise pas les fichiers `.htaccess` comme Apache, il est donc
nécessaire de créer ces URL réécrites dans la configuration disponible sur
le site. Ceci se trouve généralement dans `/etc/nginx/sites-available/your_virtual_host_conf_file`. En fonction de votre
configuration, vous devrez modifier ceci, mais au minimum, vous aurez besoin de
PHP fonctionnant comme une instance FastCGI. La configuration suivante redirige
la requête vers `public/index.php` :

```nginx
    location / {
        try_files $uri $uri/ /index.php?$args;
    }
```

Un exemple de la directive server est le suivant :

```nginx
    server {
        listen   80;
        listen   [::]:80;
        server_name www.example.com;
        return 301 http://example.com$request_uri;
    }

    server {
        listen   80;
        listen   [::]:80;
        server_name example.com;

        root   /var/www/example.com/public;
        index  index.php;

        access_log /var/www/example.com/log/access.log;
        error_log /var/www/example.com/log/error.log;

        location / {
            try_files $uri $uri/ /index.php?$args;
        }

        location ~ \.php$ {
            try_files $uri =404;
            include fastcgi_params;
            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_intercept_errors on;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }
```

> Les configurations récentes de PHP-FPM sont configurées pour écouter le
> socket unix php-fpm au lieu du port TCP 9000 sur l'adresse 127.0.0.1.
> Si vous avez des erreurs 502 bad gateway avec la configuration ci-dessus,
> essayez de mettre à jour `fastcgi_pass` pour utiliser le socket unix
> (ex: fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;) au lieu du port
> TCP.

### IIS7 (serveurs Windows)

IIS7 ne supporte pas nativement les fichiers `.htaccess`. Bien qu'il existe des
add-ons qui peuvent ajouter ce support, vous pouvez également importer des
règles htaccess dans IIS pour utiliser les réécritures natives de BabiPHP.
Pour ce faire, suivez les étapes suivantes :

1. Utilisez [l'installeur de la plateforme Web de Microsoft](http://www.microsoft.com/web/downloads/platform.aspx) pour installer
   l'URL [Rewrite Module 2.0](http://www.iis.net/downloads/microsoft/url-rewrite) ou téléchargez-le directement ([32-bit](http://www.microsoft.com/en-us/download/details.aspx?id=5747)/[64-bit](http://www.microsoft.com/en-us/download/details.aspx?id=7435)).
2. Créez un nouveau fichier appelé web.config dans votre dossier racine de BabiPHP.
3. Utilisez Notepad ou tout autre éditeur XML-safe, copiez le code suivant
   dans votre nouveau fichier web.config:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <system.webServer>
            <rewrite>
                <rules>
                    <rule name="Exclude direct access to public/*"
                      stopProcessing="true">
                        <match url="^public/(.*)$" ignoreCase="false" />
                        <action type="None" />
                    </rule>
                    <rule name="Rewrite routed access to assets(img, css, files, js, favicon)"
                      stopProcessing="true">
                        <match url="^(img|css|files|js|favicon.ico)(.*)$" />
                        <action type="Rewrite" url="public/{R:1}{R:2}"
                          appendQueryString="false" />
                    </rule>
                    <rule name="Rewrite requested file/folder to index.php"
                      stopProcessing="true">
                        <match url="^(.*)$" ignoreCase="false" />
                        <action type="Rewrite" url="index.php"
                          appendQueryString="true" />
                    </rule>
                </rules>
            </rewrite>
        </system.webServer>
    </configuration>
```

Une fois que le fichier web.config est créé avec les bonnes règles de
réécriture IIS, les liens BabiPHP, les CSS, le JavaScript, et
le reroutage devraient fonctionner correctement.
