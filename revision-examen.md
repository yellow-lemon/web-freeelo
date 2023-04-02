# Dans l'examen
- PHP (Formulaire en post)
  - Atelier 2
- API (fetch, JS)
  - Atelier 5 (Javascript)
  - Atelier 6 (API)
- BD (CRUD)
  - Atelier 3
- Théorique (MVC)
  - Atelier 4

# PHP
- [Variables (Notes du prof)](https://github.com/Cegep-joliette-info/420N462023/blob/main/notes/php/variables.md)
- [Types (Notes du prof)](https://github.com/Cegep-joliette-info/420N462023/blob/main/notes/php/types.md)
- [Superglobales (Notes du prof)](https://github.com/Cegep-joliette-info/420N462023/blob/main/notes/php/superglobales.md)
  
## GET et POST
Malgré qu'ils soient différents, get et post ce code de la même façon. \
La valeur mis dans `name="xxxx"` (input) sera le nom de la "variable". Sa valeur sera défini avec `value="xxxx"` (input). Dans un textbox, le `value` n'est pas à écrire et sera le contenu du field. Le `value` sera utilisé par exemple lorsqu'on utilise un radio button. `name` et `value` peuvent aussi être appliqué sur un button. `method`(form) permet de choisir entre get et post. La valeur par défaut est get. Le `type="submit` (button) dans le button permet d'envoyer les infos du formulaire au click. Le `action=xxxx` permet de définir où envoyer les données (redirection)

### Exemple 1 :
page1.php :
```html
<form action="page2.php" method="get">
      <input name="nom">
      <button type="submit">Bouton</button>
</form>
```

page2.php :
```php
<?php
echo($_GET['nom']);
```

### Exemple 2 :
page1.php :
```html
<form action="page2.php" method="post">
      <input name="nom">
      <button type="submit">Bouton</button>
</form>
```

page2.php :
```php
<?php
echo($_POST['nom']);
```

### Exemple avec l'utilisation du `value` :
page1.php:
```html
<p>Choisir votre classe pour le combat</p>
<form action="page2.php" method="post">
            <div class="form-check">
                <input class="form-check-input" type="radio" name="classe" id="radioGuerrier" value="Guerrier">
                <label class="form-check-label" for="radioGuerrier">Guerrier</label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="classe" id="radioVoleur" value="Voleur">
                <label class="form-check-label" for="radioVoleur">Voleur</label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="classe" id="radioMagicien" value="Magicien">
                <label class="form-check-label" for="radioMagicien">Magicien</label>
            </div>
            <button type="submit" class="btn btn-primary">Commencer</button>
</form>
```

## SESSION
En PHP, une `$_SESSION` est une variable superglobale qui permet de stocker des informations spécifiques à un utilisateur tout au long de sa session sur un site web.

Lorsqu'un utilisateur se connecte à un site, une session est créée sur le serveur web pour stocker des informations telles que l'ID de l'utilisateur, son nom d'utilisateur, son panier d'achat, sa préférence de langue, etc. Ces informations peuvent être utilisées pour personnaliser l'expérience de l'utilisateur sur le site, stocker des données temporaires et sécuriser l'accès aux pages protégées par authentification.

Pour utiliser une `$_SESSION` en PHP, il est nécessaire d'appeler la fonction `session_start()` au début de chaque page qui a besoin d'accéder aux informations de session. Cette fonction initialise la session en cours ou en crée une nouvelle si aucune n'existe déjà.

Une fois la session démarrée, les informations peuvent être stockées dans la `$_SESSION` en utilisant la syntaxe suivante :
```php
$_SESSION['nom_de_la_variable'] = 'valeur_de_la_variable';
```
Pour récupérer les données stockées dans une $_SESSION, on utilise la syntaxe suivante :
```php
Copy code
$valeur = $_SESSION['nom_de_la_variable'];
```

Enfin, pour supprimer une variable de la $_SESSION, on utilise la fonction unset() de PHP :
```php
unset($_SESSION['nom_de_la_variable']);
Il est important de noter que les données stockées dans la $_SESSION sont stockées côté serveur, ce qui les rend plus sécurisées que les cookies ou le stockage côté client. Cependant, il est également important de prendre des mesures de sécurité pour empêcher les attaques de session telles que l'injection de code malveillant.
```

## Header
Le header permet de redirigé vers un autre page.
```php
header('location: page2.php');
die();
```

# API
[Javascript (mes notes)](javascript.md)
api.php:
```js
<?php
echo ('toto');
```


```js
  //fetch('/index.php?controller=api$action=combat');
    fetch('/api.php')
      .then(response => {
        return response.text();
        // .json();
        // .blob();
      })
      .then(data => {
        document.querySelector('body').innerText = data;
    });
```

le fetch es asyncrone donc ce code ne marcherait pas :
```js

    let t = '';
    fetch('api.php')
      .then(response => {
        return response.text();
        // .json();
        // .blob();
      })
      .then(data => {
        t = data
    })
      .catch(error => {
      console.log(error);
    });
    document.querySelector('body').innerText = t;

```

---
api.php :
```js
<?php
print_r($_POST);
```

```js
document.querySelector('form').addEventListener('submit', e => {
      e.preventDefault();

      let form = document.querySelector('form');
      let formData = new FormData(form);
      //formData.append('nom', 'toto');
      let params = {
        method: 'POST',
        body: formData
      }

      fetch('api.php', params)
              .then(response => {
                if (response.ok)
                {
                  return response.text();
                }
                else
                  console.log('erreur');
              })
              .then(data => {
                console.log(data);
              })
              .catch(error => {
                console.log(error);
              });
    });
```

---
api.php :
```js
class Personnage
{
    public string $name;
}

$perso = new Personnage();
$perso->name = 'Toto';

echo json_encode($perso);
```

```js
document.querySelector('form').addEventListener('submit', e => {
      e.preventDefault();

      let form = document.querySelector('form');
      let formData = new FormData(form);
      //formData.append('nom', 'toto');
      let params = {
        method: 'POST',
        body: formData
      }

      fetch('api.php', params)
              .then(response => {
                if (response.ok)
                {
                  return response.json();
                }
                else
                  console.log('erreur');
              })
              .then(data => {
                console.log(data);
              })
              .catch(error => {
                console.log(error);
              });
    });
```

## Code
`http_response_code(401);`
- 2XX : Success
  - 200 : OK
  - 201 : Created
  - 204 : No Content

- 4XX : Erreur client
  - 400 : Bad request (Quelque chose d'invalide : un nombre trop gros, un username deja existant...)
  - 401 : Unauthorized (Pas connecté)
  - 403 : Forbidden (T'es connecté, mais tu n'as pas les accès)
  - 404 : Page not found

- 5XX : Erreur serveur

## API RESTful
règles d'une api

<!--
PHP (Formulaire en post)
API (JS)
BD (CRUD)
Théorique (MVC)
 -->
