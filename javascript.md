# Variable
Javascript n'est pas typé :
```js
let toto = '';
toto = 3;
toto += [];
console.log(toto); // 3
```

`var` ne doit plus être utilisé

## Date
ajouter des scripts pour [Day.JS](https://github.com/Cegep-joliette-info/420N462023/blob/main/notes/api/javascript.md#dayjs) \

```js
dayjs.extend(daysjs_plugin_objectSupport);

let now = dayjs();
let feteDeLaCovid = dayjs({year : 2019, month: 11, day: 31});
console.log(feteDeLaCovid);
feteDeLaCovid = feteDeLaCovid = feteDeLaCovid.add(7, 'day');
console.log(feteDeLaCovid);
```
Les mois vont de 0 à *11* \
Si on met une date comme par exemple : `{year : 2019, month: 11, day: 40}`, il ne sort pas une erreur, il avance seulement au prochain mois


# DOM
DOM = Document Object Model \
DOM permet de modifier le html avec le javascript
```js
    // <p id='toto'></p>

    document.getElementById('toto').innerHTML = 'prout';
    document.getElementById('toto').setAttribute('class', 'danger');
    document.querySelectorAll('#toto').innerText = "wesh"; // querySelector() pour un seul élément
```

```js
    let toto = document.querySelector('#toto');
    let list = toto.querySelector('ul');
    list.isnertAdjacentHTML('beforeend', "<li>Patate</li>")
```

Affiche éléments li avec le texte patate et la classe li :
```js
    <div id="toto">
        <ul></ul>
    </div>

    let toto = document.querySelector('#toto');
    let list = toto.querySelector('ul');
    for (let i = 0; i < 10; i++)
    {
        let li = document.createElement('li');
        li.classList.add('li');
        li.innerText = 'Patate';
        list.insertAdjacentElement('beforeend', li);
    }
```

Bouton qui ajoute s:
```js
<div id="toto">
    <button onclick="ajouterS()">Patate</button>
</div>

function ajouterS()
    {
        let btnPatate = document.querySelector('button');
        btnPatate.innerText += 's';
    }
```

même chose en mieux:
```js

<div id="toto">
    <button>Patate</button>
</div>

let btnPatate = document.querySelector('button');
btnPatate.addEventListener('click', function(e) {
    console.log(e);
    e.target.innerText += 's';
})


```


même chose avec un autre syntaxe:
```js
let btnPatate = document.querySelector('button');
btnPatate.addEventListener('click', (e) => {
    console.log(e);
    e.target.innerText += 's';
})
```

version plus optimisé mais moins lisible:
```js
document.querySelector('button').addEventListener('click', (e) => {
    console.log(e);
    e.target.innerText += 's';
})
```

Validation de formulaire : \
`e.preventDefault()` empêche un submit
```js
//...
```

# Norme
En haut de chaque fichier JS, il doit y avoir : `"use strict"` \
Cela empêche l'utilisation de variable non déclaré