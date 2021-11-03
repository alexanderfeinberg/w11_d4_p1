# Practice: Ordering Queries

In this short practice, you will be ordering results of **Sequelize** queries.


## Getting started

Download starter. `cd` into __server__ folder, and install dependencies using
`npm install`.

Create a __.env__ file modelled after __.env.example__, specifying the location 
of the database to be created.

Use `sequelize-cli` to run the existing migrations and seeder files.  Use 
`sqlite3` to check that the `Bands`, `Instruments`, `Musicians`, and 
`MusicianInstruments` tables exists in your database and you have seed data 
present.

In this practice you will be implementing the endpoints in __app.js__ which will
query your database for `Bands` and their associated `Musicians`. You will 
order results by singular attributes, multiple attributes, and by associated 
models.


## Step 1: Order by one attribute

The first route handler that you will work with in __app.js__ is for 
`GET /bands/latest`. It currently fetches all `Bands` and returns the results as 
a JSON response. You would like to order these results by the records' `createdAt` in 
descending order.

Complete the route handler by adding in the appropriate key to the query.

> Take a look at the [Sequelize ordering docs][ordering-basics] for examples on 
> ordering query results.

Test that the endpoint returns records in the correct order by navigating to the 
`/bands/latest` route in your browser. You should see results in the 
same order as the following. The `id`, `createdAt`, and `updatedAt`attributes 
have been stripped for brevity:

```json
[
  {
    "name": "The King River"
  },
  {
    "name": "Playin Sound"
  },
  {
    "name": "Loved Autumn"
  },
  {
    "name": "America The Piano"
  },
  {
    "name": "The Falling Box"
  }
]
```


## Step 2: Order by multiple attributes

The next route handler that you will work with is `GET /musicians/alphabetic`. 
This route fetches all `Musicians` and returns the results as a JSON response. 
You would like to order these results by `lastName`, then by `firstName`, both 
in alphabetic order.

Complete the route handler by adding in the appropriate key to the query.

Test that the endpoint returns records in the correct order by navigating to the 
`/musicians/alphabetic` route in your browser. You should see results in the 
same order as the following. The `id`, `createdAt`, `updatedAt`, and `bandId` 
attributes have been stripped for brevity:

```json
[
  {
    "firstName": "Rosemarie",
    "lastName": "Affini",
  },
  {
    "firstName": "Adam",
    "lastName": "Appleby",
  },
  {
    "firstName": "Victoria",
    "lastName": "Cremonesi",
  },
  {
    "firstName": "Aurora",
    "lastName": "Hase",
  },
  {
    "firstName": "Wilson",
    "lastName": "Holt",
  },
  {
    "firstName": "Georgette",
    "lastName": "Kubo",
  },
  {
    "firstName": "Trenton",
    "lastName": "Lesley",
  },
  {
    "firstName": "Anton",
    "lastName": "Martinovic",
  },
  {
    "firstName": "Camila",
    "lastName": "Nenci",
  },
  {
    "firstName": "Marine",
    "lastName": "Sweet",
  }
]
```


## Step 3: Order by multiple nested attributes

The final route handler that you will work with is 
`GET /bands/alphabetic-musicians`. This route fetches all `Bands` as well as 
their associated `Musicians` and returns the results as a JSON response. You 
would like to order these results first by `Band` `name`, then by the `lastName` 
of the `Musician`, then by the `firstName` of the `Musician`, all alphabetically.

Complete the route handler by adding in the appropriate key to the query.

> Take a look at the **Sequelize** eager loading docs, particularly the 
> [ordering section][order-eager-docs] for examples on how to order the nested 
> data.

Test that the endpoint returns records in the correct order by navigating to the 
`/bands/alphabetic-musicians` route in your browser. You should see results in 
the same order as the following. The `id`, `createdAt`, `updatedAt`, and 
`bandId` attributes have been stripped for brevity:

```json
[
  {
    "name": "America The Piano",
    "Musicians": [
      {
        "firstName": "Georgette",
        "lastName": "Kubo",
      },
      {
        "firstName": "Marine",
        "lastName": "Sweet",
      }
    ]
  },
  {
    "name": "Loved Autumn",
    "Musicians": [
      {
        "firstName": "Aurora",
        "lastName": "Hase",
      }
    ]
  },
  {
    "name": "Playin Sound",
    "Musicians": [
      {
        "firstName": "Trenton",
        "lastName": "Lesley",
      },
      {
        "firstName": "Camila",
        "lastName": "Nenci",
      }
    ]
  },
  {
    "name": "The Falling Box",
    "Musicians": [
      {
        "firstName": "Adam",
        "lastName": "Appleby",
      },
      {
        "firstName": "Wilson",
        "lastName": "Holt",
      },
      {
        "firstName": "Anton",
        "lastName": "Martinovic",
      }
    ]
  },
  {
    "name": "The King River",
    "Musicians": [
      {
        "firstName": "Rosemarie",
        "lastName": "Affini",
      },
      {
        "firstName": "Victoria",
        "lastName": "Cremonesi",
      }
    ]
  }
]
```


## Congratulations!

You are now able to order the results of **Sequelize** queries by singular, 
multiple, and nested attributes.


[ordering-basics]: https://sequelize.org/master/manual/model-querying-basics.html#ordering
[order-eager-docs]: https://sequelize.org/master/manual/eager-loading.html#ordering-eager-loaded-associations