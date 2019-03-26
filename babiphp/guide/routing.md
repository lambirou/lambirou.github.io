# Routing

`class` BabiPHP\Routing\\**Router**

Le Routing est une fonctionnalité qui fait correspondre les URLs aux actions du controller. En définissant des routes, vous pouvez séparer la façon dont votre application est intégrée de la façon dont ses URLs sont structurées.

Le Routing dans BabiPHP englobe aussi l’idée de routing inversé, où un tableau de paramètres peut être transformé en une URL. En utilisant le routing inversé, vous pouvez reconstruire la structure d’URL de votre application sans mettre à jour tous vos codes.

## Tour Rapide

Cette section va vous apprendre les utilisations les plus habituelles du Router de BabiPHP. Typiquement si vous voulez afficher quelque chose en page d’accueil, vous ajoutez ceci au fichier `config/routes.php`:

```php
use \BabiPHP\Routing\Router;

Router::get('blog.home', '/', 'blog@index');
Router::route('blog.portfolio', '/portfolio/{name}', 'blog@portfolio');
Router::route('blog.post', '/post', 'blog@post')->allows('GET');
Router::post('blog.ajax', '/ajax', 'blog@ajax')->allows(['GET']);
```
