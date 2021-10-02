# MongoDB Quick Guide

## Author

- [@nithinhacks](https://github.com/nithinhacks)

## Basic commands

<strong>mongosh</strong>:
    Open a connection to your local MongoDB instance. All other commands will be run within this mongosh connection.
___

<strong>show dbs</strong>: 
    Show all databases in the current MongoDB instance.
___

<strong>use `<dbname>`</strong>: 
    switch to the database provided by dbname.<br>
example:<br>
`use myDatabase`<br>Switch to myDatabase
___

<strong>db</strong>: 
    Show current database name.
___

<strong>cls</strong>: 
    Clear the terminal screen.
___

<strong>show collections</strong>: 
    Show all collections in the current database.
___

<strong>db.dropDatabase()</strong>:
    Delete the current database.
___

<strong>exit</strong>: 
    Exit the mongosh session.
___

## Create
Each of these commands is run on a specific collection<br>
`db.<collectionName>.<command>`
___

<strong>insertOne</strong>: 
    Create a new document inside the specified collection<br>
example:<br>
`db.users.insertOne({ name: “Nithin” })`<br>Add a new document with the name of Nithin into the users collection.
___

<strong>insertMany</strong>:
    Create multi new documents inside a specific collection.<br>
example:<br>
`db.users.insertMany([{ age: 26 }, { age: 20 }])`<br>
Add two new documents with the age of 26 and 20 into the users collection
___

## Read
Each of these commands is run on a specific collection<br>
`db.<collectionName>.<command>`
___

<strong>find</strong>:
    Get all documents.<br>
example:<br>
`db.users.find()`<br>
Get all users
___

<strong>find(`<filterObject>`)</strong>:
    Find all documents that match the filter object.<br>
example:<br>
`db.users.find({ name: “Nithin” })`<br>
Get all users with the name Nithin<br>
`db.users.find({ “address.street”: “visakhapatnam” })`<br>
Get all users whose adress field has a street field with the value visakhapatnam
___

<strong>find(`<filterObject>`, `<selectObject>`)</strong>:
    Find all documents that match the filter object but only return the field specified in the select object.<br>
example:<br>
`db.users.find({ name: “Nithin” }, { name: 1, age: 1 })`<br>
Get all users with the name Nithin but only return their name, age, and _id<br>
`db.users.find({}, { age: 0 })`<br>
Get all users and return all columns except for age
___

<strong>findOne</strong>:
    The same as find, but only return the first document that matches the filter object.<br>
example:<br>
`db.users.findOne({ name: “Nithin” })`<br>
Get the first user with the name Nithin
___

<strong>countDocuments</strong>:
    Return the count of the documents that match the filter object passed to it.<br>
example:<br>
`db.users.countDocuments({ name: “Nithin” })`<br>
Get the number of users with the name Nithin
___

## Update

Each of these commands is run on a specific collection<br>
`db.<collectionName>.<command>`
___

<strong>updateOne</strong>:
    Update the first document that matches the filter object with the data passed into the second parameter which is the update object<br>
example:<br>
`db.users.updateOne({ age: 20 }, { $set: { age: 21 } })`<br>
Update the first user with an age of 20 to the age of 21
___

<strong>updateMany</strong>:
    Update all documents that matches the filter object with the data passed into the second parameter which is the update object<br>
example:<br>
`db.users.updateMany({ age: 12 }, { $inc: { age: 3 } })`<br>
Update all users with an age of 12 by add 3 to their age
___

<strong>replaceOne</strong>:
    Replace the first document that matches the filter object with the exact object passed as the second parameter. This will completely overwrite the entire object and not just update individual fields.<br>
example:<br>
`db.users.replaceOne({ age: 12 }, { age: 13 })`<br>
Replace the first user with an age of 12 with an object that has the age of 13 as its only field
___

## Delete

Each of these commands is run on a specific collection<br>
`db.<collectionName>.<command>`
___

<strong>deleteOne</strong>:
    Delete the first document that matches the filter object<br>
example:<br>
`db.users.deleteOne({ age: 20 })`<br>
Delete the first user with an age of 20
___

<strong>deleteMany</strong>:
    Delete all documents that matches the filter object
example:<br>
`db.users.deleteMany({ age: 12 })`<br>
Delete all users with an age of 12
___

## Complex Filter Object

Any combination of the below can be use inside a filter object to make complex queries
___

<strong>$eq</strong>:
    Check for equality<br>
example:<br>
`db.users.find({ name: { $eq: “Nithin” } })`<br>
Get all users with the name Nithin
___

<strong>$ne</strong>:
    Check for not equal<br>
example:<br>
`db.users.find({ name: { $ne: “Nithin” } })`<br>
Get all users with a name other than Nithin
___

<strong>$gt / $gte</strong>:
    Check for greater than and greater than or equal to<br>
example:<br>
`db.users.find({ age: { $gt: 12 } })`<br>
Get all users with an age greater than 12<br>
`db.users.find({ age: { $gte: 15 } })`<br>
Get all users with an age greater than or equal to 15
___

<strong>$lt / $lte</strong>:
    Check for less than and less than or equal to<br>
example:<br>
`db.users.find({ age: { $lt: 12 } })`<br>
Get all users with an age less than 12<br>
`db.users.find({ age: { $lte: 15 } })`<br>
Get all users with an age less than or equal to 15
___

<strong>$in</strong>:
    Check if a value is one of many values<br>
example:<br>
`db.users.find({ name: { $in: [“Nithin”, “John”] } })`<br>
Get all users with a name of Nithin or John
___

<strong>$nin</strong>:
    Check if a value is none of many values<br>
example:<br>
`db.users.find({ name: { $nin: [“Nithin”, “John”] } })`<br>
Get all users that do not have the name Nithin or John
___

<strong>$and</strong>:
    Check that multiple conditions are all true<br>
example:<br>
`db.users.find({ $and: [{ age: 12 }, { name: “Nithin” }] })`<br>
Get all users that have an age of 12 and the name Nithin<br>
`db.users.find({ age: 12, name: “Nithin” })`<br>
This is an alternative way to do the same thing. You do not need $and.
___

<strong>$or</strong>:
    Check that one of multiple conditions is true<br>
example:<br>
`db.users.find({ $or: [{ age: 12 }, { name: “Nithin” }] })`<br>
Get all users with a name of Nithin or an age of 12
___

<strong>$not</strong>:
    Negate the filter inside of $not<br>
example:<br>
`db.users.find({ name: { $not: { $eq: “Nithin” } } })`<br>
Get all users with a name other than Nithin
___

<strong>$exists</strong>:
    Check if a field exists.<br>
example:<br>
`db.users.find({ name: { $exists: true } }`<br>
Get all users that have a name field
___

<strong>$expr</strong>:
    Do comparisons between different fields.<br>
example:<br>
`db.users.find({ $expr: { $gt: [“$balance”, “$debt”] } })`<br>
Get all users that have a balance that is greater than their debt
___

## Complex Update Object

Any combination of the below can be use inside an update object to make complex updates
___

<strong>$set</strong>:
    Update only the fields passed to $set. This will not affect 
any fields not passed to $set<br>
example:<br>
`db.users.updateOne({ age: 12 }, { $set: { name: “Hi” } })`<br>
Update the name of the first user with the age of 12 to the value Hi
___

<strong>$inc</strong>:
    Increment the value of the field by the amount given<br>
example:<br>
`db.users.updateOne({ age: 12 }, { $inc: { age: 2 } })`<br>
Add 2 to the age of the first user with the age of 12
___

<strong>$rename</strong>:
    Rename a field<br>
example:<br>
`db.users.updateMany({}, { $rename: { age: “years” } })`<br>
Rename the field age to years for all users
___

<strong>$unset</strong>:
    Remove a field<br>
example:<br>
`db.users.updateOne({ age: 12 }, { $unset: { age: “” } })`<br>
Remove the age field from the first user with an age of 12
___

<strong>$push</strong>:
    Add a value to an array field<br>
example:<br>
`db.users.updateMany({}, { $push: { friends: “John” } })`<br>
Add John to the friends array for all users
___

<strong>$pull</strong>:
    Remove a value from an array field<br>
example:<br>
`db.users.updateMany({}, { $pull: { friends: “Mike” } })`<br>
Remove Mike from the friends array for all users
___

## Read Modifiers

Any combination of the below can be added to the end of any read operation
___

<strong>sort</strong>:
    Sort the results of a find by the given fields<br>
example:<br>
`db.users.find().sort({ name: 1, age:- 1 })`<br>
Get all users sorted by name in alphabetical order and then if any names are the same sort by age in reverse order
___

<strong>limit</strong>:
    Only return a set number of documents<br>
example:<br>
`db.users.find().limit(2)`<br>
Only return the first 2 users
___

<strong>skip</strong>:
    Skip a set number of documents from the beginning<br>
example:<br>
`db.users.find().skip(4)`<br>
Skip the first 4 users when returning results
___
