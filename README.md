Laravel Todo List API
================

A simple todo list API built with Laravel 4 used to teach myself and somefriends how create a restful application with Laravel 4.

## A little bit about this project:

* PHP 5.4.x
* Laravel 4.2.x (Framework)
* MySQL
* PHPUnit (Tests)

#### Summary

* [Database](#about-database)
* [The DAMN MVP](#the-damn-mvp)
* [Using this API](#using-this-api)
* [API Routes](#about-api-routes)
* [Notes](#notes)

## About Database

In this case, we use MySQL, but if you want can use PostgreSQL or others databases.

This is a simple TodoList, in other words, we just need a table to storage our tasks and just it, but we implements some auth with user.

###### Table Name: Tasks

Field | Type | Null | Key | Default
--- | --- | --- | --- | ---
id | INT(10) | NO | PRI | NULL
title | VARCHAR(255) | NO | | NULL
status | BOOLEAN | NO | | 0
user_id | INT(10) | NO | | NULL
created_at | TIMESTAMP | NO | | 0
updated_at | TIMESTAMP | NO | | 0

###### Table Name: Users

Field | Type | Null | Key | Default
--- | --- | --- | --- | ---
id | INT(10) | NO | PRI | NULL
username | VARCHAR(100) | NO | | NULL
email | VARCHAR(100) | NO | | NULL
password | VARCHAR(255) | NO | | NULL
key | VARCHAR(20) | NO | | NULL

## The DAMN MVP
The Application need support the **HTTP Methods** like **GET**, **POST**, **PUT** and **DELETE**.

This way we have some routes to create, read, update and delete.

But nothing it's so easy, for add a minimal security, we need to send a **ApiKey** with data to validate if we have permission to add, update or remove that tasks.

To do that, we need create an **"user"**.

The user have a **username**, **email**, **password** and the **ApiKey** of course.

This way we secure that user modify tasks than belogs him, with the user_id key (in tasks table).

> ApiKey it's just a string of characteres generated by [uniqid()](http://php.net/manual/en/function.uniqid.php).

## Using this API

Very easy.

Install all dependencies with [composer](https://getcomposer.org/)
```
composer install
```

Add database params into `app/config/database.php`
``` php
'mysql' => array(
  'driver'    => 'mysql',
  'host'      => 'localhost',
  'database'  => 'Your_database_name',
  'username'  => 'username',
  'password'  => 'password',
  'charset'   => 'utf8',
  'collation' => 'utf8_unicode_ci',
  'prefix'    => '',
)
```

Enable migration
```
php artisan migrate:install
```

Execute all migrations of project
```
php artisan migrate
```

Seed database with some fake data (Not really necessary)
```
php artisan db:seed
```

## About API Routes

Description | Method | Url
--- | --- | ---
Root of Application | GET | `/api`
Get all tasks of application | GET | `/api/tasks`
Create a new Task | POST | `/api/tasks`
Get a single where's ID equals :id | GET | `/api/tasks/:id`
Update a single where's ID equals :id | PUT | `/api/tasks/:id`
Delete a single task where's ID equals :id | DELETE | `/api/tasks/:id`

## Notes

**Remember:** To user the API, you need to have an user into Database.
In the seed, contains a guest user, with ApiKey `54a9bf1b0dbce`.

We use [Laravel 4 Generators](https://github.com/JeffreyWay/Laravel-4-Generators) by [Jeffrey Way](https://github.com/JeffreyWay), to improve our speed in development.