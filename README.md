# sf4-base-secure

## Creation :
<pre><code>composer create-project symfony/skeleton base-secure
cd base-secure
composer require symfony/web-server-bundle --dev</code></pre>

## Base :
<pre><code>composer require annotations symfony/security-bundle
composer require symfony/swiftmailer-bundle
composer require --dev maker profiler sensiolabs/security-checker reqcheck</code></pre>

## BDD :
<pre><code>composer require doctrine
composer require --dev doctrine/doctrine-fixtures-bundle fzaninotto/faker</code></pre>

## Front :
<pre><code>composer require twig asset form symfony/validator</code></pre>

