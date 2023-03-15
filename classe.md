```php

namespace Main;

class User
{
  public const ROLE_USER = 0;
  public const ROLE_ADMIN = 1;

  public int $id;
  public string $username;
  public int $password;
  public int $role;

  public function __construct (?string $username = null, ?string $password = null)
  {
    $this->username = $username;
    $this->username = $username ?? "default";
    //...
    $this->role = self::ROLE_USER;
  }

  public function hashPassword() : void
  {
    $this->password = $this->password . '123';
  }



}

```

```php
class Student extends User
{
  public function __construct($username, $password)
  {
    parrent::__construct($username, $password);
  }

  public function hashPassword() : void
  {
    $this->password = $this->password . '456';
  }
}
```
- keyword `abstract` au début empêche de créer un objet de ce type
- keyword `final` empêche les dérivés de cette classe

# Traits

## Exemple
```php
<?php
namespace Traits;

trait Account
{
  public string $username;
  public string $password;
}

public function newUsername($username): void
{
  if (strlen($username) == 7)
  {
    $this->username = $username;
  }
}
```

```php
<?php

namespace Traits;

trait Student
{
  public string $da;
}

public function newUsername($username): void
{
  if (strlen($username) == 7)
  {
    $this->username = $username;
  }
}
```

```php
<?php

namespace Traits;

class StudentAccount
{
  use Student, Account
  {
    Student::newUsername insteadof Account;
  };
}


```