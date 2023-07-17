# E-Commerce Database

## Table of Contents

1. [Description](#description)
2. [Demo](#demo)
2. [Installation](#installation)
3. [User Story](#user-story)
3. [Acceptance Criteria](#acceptance-criteria)
3. [Comments](#comments)
4. [License](#license)

## Description

This is the back-end for an e-commerce database, using an Express.js API to use Sequelize to interact with a MySQL database. The database can be updated using the API URLs. An e-commerce site can store their data about many products, and organize them with categories and tags.

## Demo

[Video Demo](https://drive.google.com/file/d/1CM9V_vlv-OFbEJ-1kZVxge8e89LJs9fP/view)

## Installation

1. Download a copy of the repository.
2. In the command line, navigate to the repo and run `npm install`.
3. Make sure you have [MySQL](https://www.mysql.com/) installed and set up.  See [this installation guide](https://coding-boot-camp.github.io/full-stack/mysql/mysql-installation-guide) for any help.
4. Log into your MySQL Shell, and run `source db/schema.sql`, then exit the shell.
5. For some sample data to start, run `npm run seed`.
7. In the repo folder, create a file called .env containing the following. Replace "root" and "localhost" with your username and host if needed, and insert your own password.
```
DB_DATABASE='ecommerce_db'
DB_PASSWORD=''
DB_USER='root'
```
8. Now you can run `npm start` to get started!

## User Story

```md
AS A manager at an internet retail company
I WANT a back end for my e-commerce website that uses the latest technologies
SO THAT my company can compete with other e-commerce companies
```

## Acceptance Criteria

```md
GIVEN a functional Express.js API
WHEN I add my database name, MySQL username, and MySQL password to an environment variable file
THEN I am able to connect to a database using Sequelize
WHEN I enter schema and seed commands
THEN a development database is created and is seeded with test data
WHEN I enter the command to invoke the application
THEN my server is started and the Sequelize models are synced to the MySQL database
WHEN I open API GET routes in Insomnia for categories, products, or tags
THEN the data for each of these routes is displayed in a formatted JSON
WHEN I test API POST, PUT, and DELETE routes in Insomnia
THEN I am able to successfully create, update, and delete data in my database
```


## Comments

1. I was annoyed by the repetitive data coming back, for example, seeing both `category_id: 9` and `category: {id: 9}`.  So in the routes, I changed it from having just `include: Category` to the following.
    ```
    {
      include: {
        model: Category,
        attributes: ['id','category_name']
      },
      attributes: { exclude: 'category_id' }
    }
    ```
    It makes the GET routes a little more complex, but I like having the data coming back being cleaner.  It's especially nicer with the many-to-many relationship of the products and tags.

2. In the [Sequelize documentation](https://sequelize.org/docs/v6/core-concepts/assocs/#options-1), it says that `onDelete` is by default set to `SET NULL`. But when I didn't include that property explicitly, it behaved like it was set to `RESTRICT` instead.  I would get a 500 error when attempting to delete a category that had products in it. I'm not sure where the on-delete behavior was changed.


## License

The MIT License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)