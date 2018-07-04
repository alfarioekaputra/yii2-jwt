# yii2-jwt

JWT implementation for Yii2 Authorization process

For details see [JWT official website](https://jwt.io/introduction/).

## Usage

There is only one trait - *UserTrait* - which gives you 5 methods for
authorization and JWT-management in User model

Set up:

In controller:

```PHP
<?php

// ...

use yii\filters\auth\HttpBearerAuth;

class BearerAuthController extends \yii\rest\ActiveController
{
    public function behaviors()
    {
        return array_merge(parent::behaviors(), [
            'bearerAuth' => [
                'class' => HttpBearerAuth::className()
            ]
        ]);
    }
}
```

In User model:

```PHP
<?php

// ...

use yii\db\ActiveRecord;
use yii\web\IdentityInterface

class User extends ActiveRecord implements IdentityInterface
{
    // Use the trait in your User model
    use \damirka\JWT\UserTrait;

    // Override this method
    protected static function getSecretKey()
    {
        return 'someSecretKey';
    }

    // And this one if you wish
    protected static function getHeaderToken()
    {
        return [];
    }

    // ...
}
```
