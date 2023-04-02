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

# Code
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

# API RESTful
règles d'une api