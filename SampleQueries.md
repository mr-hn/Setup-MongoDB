# Running simple queries on Mongo
Once MongoDB is setup and data is loaded by following the steps in SetupMongoDB.md, we run some simple queries.   

- ### Starting the server  

  Start the server by 
  `mongod --dbpath /home/harish/myPackages/MongoDB/databases`  
  
  In the console, type `show dbs` to see all available databases.   
  In our case, for the dataDump file that we loaded, it will be   
  `journaldev  0.000GB`   
  `local       0.000GB`   
  `sample      0.004GB`   
  `test        0.000GB`   
  
  Go into sample `use sample`.   
  View the collections inside the database by `show collections` for which the output will be   
  `collection`   
  `users`   
  
- ### Running basic commands

  `db.users.count()` will give you a count of records in `users` collection.   
  
  `db.users.findOne()` will return the first record/tweet in the DB.   
  One can see the semi-structured tweet data available in the hierarchial tree format.   
  
  The query condition can be passed in curly braces.   
  `db.users.find({user_name : "Tonkatol"})` lists out all tweets made by the user `Tonkatol`.   
  
- ### Aggregation conditions    
  `db.users.find({"tweet_followers_count":{$gt:1000},"tweet_mentioned_count":{$lt:1}}).count()` shows the number of tweets which has a follower count greater than 1000 but not mentioned even once.   
  
  To see all tweets that contain the text "FIFA"
  `db.users.find({$text:{$search: "FIFA"}}).pretty()`   
  
More commands can be explored [here](https://docs.mongodb.com/manual/aggregation/).
