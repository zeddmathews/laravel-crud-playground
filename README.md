# **laravel-crud-playground**
**Practice Laravel + Vue + Inertia + PostgreSQL project**

### notes
Base project created with laravel new
Edited laravel .env file to use pgsql instead of sqlite
basic migration: php artisan migrate to put into effect changes and create default tables
app run: php artisan serve
composer run dev (composer.json dev script, includes artisan serve, queue, npm run dev (see package.json))

### definitions
`$foo->bar();` call the `bar()` method of object `$foo`
`$foo->bar;` get the `bar` property of object `$foo`
Object Access Operator: `->` used for calling methods on an operator or accessing properties of an object
Scope Resolution Operator: `::` Calling static methods, accessing constants, accessing class names in facades
**<sup>Facades provide a static interface to classes that are available in the applications's service container</sup>**