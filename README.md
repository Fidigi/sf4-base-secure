# sf4-base-secure

## Fonctionnalité :

### Les routes
<pre>
  security_register          ANY      ANY      ANY    /security/signup                   
  security_activate          ANY      ANY      ANY    /security/activate/{tokenValue}    
  security_login             ANY      ANY      ANY    /security/signin                   
  security_logout            ANY      ANY      ANY    /security/signout                  
  security_lost_password     ANY      ANY      ANY    /security/lost                     
  security_reset_password    ANY      ANY      ANY    /security/reset/{tokenValue}  
</pre>
#### security
##### signup
création de compte

##### activate
Activation de compte en jouant le lien de l'email d'activation

##### signin
Se connecter à l'application via son email ou son user name

config/packages/security.yaml
<pre>
        main:
            anonymous: true
            guard:
                authenticators:
                    - App\Security\LoginFormAuthenticator
            user_checker: App\Security\UserChecker
            logout:
                path: security_logout
                target: app_home
            access_denied_handler: App\Security\Handler\AccessDeniedHandler
</pre>

app/Repository/UserRepository.php
<pre>
public function findOneByUsernameOrEmail($username)
</pre>

##### signout
Se déconnecter de l'application

##### lost
Faire une demande de changement de mot de passe pour un mot de passe perdu. Ce qui envoie un email.

##### reset
Changement du mot de passe possible en jouant le lien de l'email du "lost"

## Points de configuration :

### Les roles user

app/Service/UserManager.php
<pre>
class UserManager
{
    const USER_ROLE_USER = 'ROLE_USER';
    const USER_ROLE_MOD = 'ROLE_MOD';
    const USER_ROLE_ADMIN = 'ROLE_ADMIN';
    
    ...
}
</pre>
config/packages/security.yaml
<pre>
    role_hierarchy:
        ROLE_MOD: ROLE_USER
        ROLE_ADMIN: ROLE_MOD
</pre>

### Les tokens
app/Service/TokenManager.php
<pre>
class TokenManager
{
    const TOKEN_TYPE_REGISTER = 'REG';
    const TOKEN_TYPE_LOST = 'LOST';
    const TOKEN_TYPE_API = 'API';

    const TOKEN_REGISTER_DURATION = 'now +1 day';
    const TOKEN_LOST_DURATION = 'now +10 min';
    const TOKEN_API_LONG_DURATION = 'now +1 month';
    const TOKEN_API_SHORT_DURATION = 'now +10 hours';
    
    ...
}
</pre>
## Installation :

### Creation :
<pre><code>composer create-project symfony/skeleton base-secure
cd base-secure
composer require symfony/web-server-bundle --dev</code></pre>

### Base :
<pre><code>composer require annotations symfony/security-bundle
composer require symfony/swiftmailer-bundle
composer require --dev maker profiler sensiolabs/security-checker reqcheck</code></pre>

### BDD :
<pre><code>composer require doctrine
composer require --dev doctrine/doctrine-fixtures-bundle fzaninotto/faker</code></pre>

### Front :
<pre><code>composer require twig asset form symfony/validator</code></pre>

