## Variable
```php
$var = 1;
$Var =2;
```

### Type
```php
$bool = true;
$int = 1234;
$oct = 0123; // Zero au début
$hex = 0x1A; // 0x au début
$bin = 0b010101010 // Ob au début
$int2 = 1_1987_682;
$int3 = PHP_INT_MAX;

```

#### float
```php
echo (1.6); // 1.6
echo('<br>');
echo (8-6.4); // 1.6

$res = 1.6 == 8-6.4;
var_dump($res); // false
```
à la place, il faut faire
```php
const EPSILON = 0.00001;

if (abs((8-6.4) - 1.6) < EPSILON)
{
    
}
```

#### string
```php
$name = 'Toto';
$foo1 = 'Mon nom est' . $name;
$foo2 = 'Mon nom est $name'; // N'affiche pas la valeur de name
$foo3 = "Mon nom est $name";
```

#### Tableau
```php
$tab1 = array(1, 2, 3);
$tab2 = [1,2,3];

echo('<pre>');
print_r($tab1);
print_r($tab2);
```

```php
$tab = [1, 2, 3];
$tab[0] = 'asdf';
$tab[1] = true;
$tab[2] = [4, 5, 6];
$tab[10] = 12;
$tab['toto'] = 'prout';
$tab[] = 1; // Ajoute un élément au bout;
```

#### Date
```php
$demain = new DateTime(); // Maintenant
$demain->add(new DateInterval('P1D'));
print_r($demain);

```

### Typage strict
```php
declare(strict_type=1);
```

```php
$a = '1' == 1;
```

### Transtypage
```php
var_dumb(intval("42asd")); // 42
var_dumb(floatval("asd")); // 0, car il n'arrive pas à convertir
```

## Concactenation
```php
echo("hello" . 1);
```


## Comparaison
`==` compare la valeur. 0, false, '', null et [] sont égales \
`===` compare aussi le type

## Function
```php
function addition(int $nb1, int $nb2): int
{
  return $nb1 + $nb2;
}

echo(addition(1, 2));
```

```php
function inc(int $a): void //Par valeur
{ 
  $a++
} 

function inc(int &$a): void //Par référence
{ 
  $a++
} 
```

```php
function diviser (int $nb1, int $nb2): ?int //le ? permet de retourner un int ou un null. Possible de faire aussi int|null
{
  //...
}
```

```php
function add (int ...$numbers): int
{
  $somme = 0;
  for ($i = 0; $i < count($numbers); $i++)
  {
    $somme += $numbers[$i];
  }
  return $somme;
}

echo(add(1, 2, 3, 4, 5));
echo(add(...$tab));
```

```php
$bonjour = "wesh";

function bonjourMonde()
{
  global $bonjour;
  echo($bonjour);
}
```

## For each
```php
foreach ($numbers as $number)
{
  $somme += $number;
}
return $somme;

foreach ($numbers as $key => $number) //pour lindice
{
  $somme += $number;
}

foreach ($numbers as $key => &$number) //pour la référence
{
  $somme += $number;
}
```

```php
$tab = [1, 2, 3];

foreach ($tab as &$n)
{
  $n *= 2;
}

print_r($tab);
```

## If
```php
$a = 2;
$b = 4;

if ($a > $b)
{
  echo('Plus petit');
} 
elseif ($a < $b)
{
  echo('Plus grand');
}
else
{
  echo('prout');
}
```

## Match
```php
$age = 18;
$prix = match($age)
{
  16 => 16,
  20 => 18
};

prix = match(true)
{
  &age < 12 => 6,
  &age > 60 => 8,
  default => 10
};
```

## Opérateur null
```php
$nom = null;
$nom = $nom ?? "anonyme"; //Si la gauche est null, prend la droite
```

## Comparateur <=>
```php
echo(1<=>2); //-1
```

## Affichage
```html
<?php
$nom = "Toto";

?>

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
  Bonjour <?= echo($nom) ?>
</body>
</html>
```

```html
<?php
$nom = "Toto";

?>

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
  <?= if ($nom != "") { ?>
  Bonjour <?= echo($nom) ?>
  <?= } ?>
</body>
</html>
```

# Superglobal
readonly
```php
<?= 
printr($_SERVER);
printr($_COOKIE);
printr($_GET);
>
```

## Cookie
```php
setcookie('bleu', 'rouge');

setcookie(
    string $name,
    string $value = "",
    int $expires_or_options = 0,
    string $path = "",
    string $domain = "",
    bool $secure = false,
    bool $httponly = false
): bool

printr($_COOKIE);

setcookie('blue', '', -1);
```

## GET et POST
Chaque paramètre GET est séparé par un & \
`https://search.brave.com/search?q=test&source=desktop` \
`q=test` et `source=desktop`

printr($_GET);

```php
<form method="post">
  <?= isset($_POST['name']) ? "Bonjour {$_POST['name']}" : '' ?>
  <div>
    <label for="name">Nom</label>
    <input type="text" name="name" id="name">
    <button class="btn btn-primary">Envoyer</button>
  </div>
</form>
```

Envoyé la requête vers un autre formulaire
```php
<form method="post" action="name.php">
  <?= isset($_POST['name']) ? "Bonjour {$_POST['name']}" : '' ?>
  <div>
    <label for="name">Nom</label>
    <input type="text" name="name" id="name">
    <button class="btn btn-primary">Envoyer</button>
  </div>
</form>
```
dans name.php

```php
<?php
if (!isset($_POST['name']))
{
  header('location: index.php');
  die();
}
echo("Bonjour {$_POST['name']}");
?>
```

```php
$nb1 = $_POST['nb1'];
```

## Session
pas en read only
session_start();

<?= print_r($_COOKIE) ?>

$_SESSION['username'] = 'toto';

$_SESSION = [];
session_destroy();

## Random
```php
rand(int $min, int $max)
```



