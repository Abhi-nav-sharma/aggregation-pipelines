# Mongo - Aggregation pipelines 

## Problem

### Data

create a mock movies table in sequel and mongodb which has 500 documents which has following columns/fields

- id
- movie_name
- movie_genre
- production_year ( between 1990 to 2020)
- budget ( 9000 to 20000)
- rating ( 0 - 10 )
- rated ( PG or G )
- language
- genres

#### create an aggregation query for the following
- rating is atleast 8
```js
  db.movies.aggregate([{$match:{rating:{$gte:8}}}])
```
- genres do not contain "Thriller" or "Romance"
```js
db.movies.aggregate([{$match:{movie_genre:{$nin:['Thriller','Romance']}}}])
```
- rated "PG"
```js
db.movies.aggregate([{$match:{rated:'PG'}}])
```
- languages contain English or French
```js
db.movies.aggregate([{$match:{$or:[{language:'English'},{language:'French'}]}}])
```
- production_year after 2012
```js
db.movies.aggregate([{$match:{production_year:{$gt: 2012}}}])
```

### you have been given a task by your manager
- you have a huge collection of data
- you need to find the total number of duplicates that are found on against a key
- here the duplicates are formed from the name
```js
{ name: "aman", id: 1 } , { name: "albert", id : 2 } { name: "aman", id: 3 } , { name: "albert", id : 4 }  { name :"nrupul", id: 5 }
```
- in this case required output is
- { name: "aman", duplicates: 1 }, { name: "albert", duplicates: 1 } ,{ name: "nrupul", duplicates: 0 }
- use aggregations and try to solve this

```js
db.data.aggregate([{$group:{_id:'$name',duplicate:{$sum:1}}}])
```

### 3
- you have a set of data in a collection in the following manner ```
- city
- email
- order_id ```
- there can be duplicate emails
- you need to filter out the total no of unique emails on each city
- you can use aggregation for this

```js
db.city.aggregate([ {$group : { _id : "$email", count : {$sum :1}}},{$project : { Emails : "$_id", "_id" : 0, Count : "$count" } }  ])
```