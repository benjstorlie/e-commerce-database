# E-Commerce Database

## Table of Contents

1. [Description](#description)
2. [Demo](#demo)
2. [Installation](#installation)
3. [Comments](#comments)

## Description

## Demo


## Installation

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