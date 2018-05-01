### Confirmation

#### Signup confirmation

Get a verification token. Use it in an url and set that url in an e-mail to the user.

```php
// Create a new $user

$auth = new Auth();
$confirmationToken = $auth->getConfirmationToken($user, 'signup');

$host = $_SERVER['HTTP_HOST'];
$url = "http://$host/confirm.php?token=$confirmationToken";
    
mail(
  $user->getEmail(),
  "Welcome to our site",
  "Please confirm your account by visiting $url"
);
```

Use the confirmation token to fetch and verify the user

```php
// --- confirm.php

$auth = new Auth();
$user = $auth->fetchUserForConfirmation($_GET['token'], 'signup');

if (!$user) {
    http_response_code(400);
    echo "The token is not valid";
    exit();
}

// Process the confirmation
// ...
```

#### Forgot password

Get a verification token. Use it in an url and set that url in an e-mail to the user.

Setting the 3th argument to `true` will use the hashed password of the user in the checksum. This means that the token
will stop working once the password is changed.

```php
// Fetch $user by e-mail

$auth = new MyAuth();
$confirmationToken = $auth->getConfirmationToken($user, 'reset-password', true);

$host = $_SERVER['HTTP_HOST'];
$url = "http://$host/reset.php?token=$confirmationToken";

mail(
  $user->getEmail(),
  "Password reset request",
  "You may reset your password by visiting $url"
);
```

Use the confirmation token to fetch and verify resetting the password

```php
$auth = new MyAuth();
$user = $auth->fetchUserForConfirmation($_GET['token'], 'reset-password', true);

if (!$user) {
    http_response_code(400);
    echo "The token is not valid";
    exit();
}

// Show form to set a password
// ...
```
