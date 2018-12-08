# Introduction to Databases

A quick introduction to databases. This guide works best if you have a solid understanding of Object-Oriented Programming.

### Database
 A database is an organized collection of information. This information is stored in a systematic way to allow for sensible retrieval of data. A database can be visualized like a spreadsheet, where the first set of columns denote what type of information is stored, and every row following will contain the information of that type. For example:
 ```
 +========================+
 | first_name | last_name |
 |============+===========|
 | Jonathan   | Smith     |
 |========================|
 ```

### Table
A Table is a "section" of a database that holds information about a specific kind of information relating to a single topic. For example: a Users table would hold information about all the users of a website. This information is stored in rows that each pertain to one _instance_ of that type of information Each instance or row of a table is known as a record.

### Schema
Schema is a fancy word for blueprint or template. A schema represents how something should be mocked up, or what _template_ it should adhere to. This is the same concept of creating classes in most object oriented programming languages. The class definition is the schema for that kind of object. Below is a simple schema for a standard user object.

```
// A simple class in JavaScript (ES6)
class User {
  constructor(email, name) {
     this.email = email;
     this.name = name;
     this.status = 'active';
  }
}```

So how does a schema look for a database? We use Structured Query Language (SQL) to communicate with databases. Notice that when we create the table/schema below, we use a plural name for the table, instead of a singular name.

```
CREATE TABLE users (
  Name varchar(255),
  Username varchar(255),
  Status varchar(255)
);
```


### Record
A record is a complete set of information that is comprised of different fields of data (first_name, last_name, email, etc). Think of a single row in a database as its own record, or in Object-Oriented Programming terms, an _instance_.

### Primary Key
A primary key is a column of a table that serves as the indentifier for each individual row within that table. Generally, this column is called "id" and is an integer. Each value provided for a primary key must be unique, otherwise the system doesn't work. **Note**: Usually this key is programmed to be a value that auto-increments with the creation of each record on the table.

### Foreign Key
A foreign key is a column of a table that serves as a reference to a row of an external table. Foreign keys are often used to allow systems to keep track of possession and associations. For example: what author wrote which books?  


Here are Primary Keys and Foreign Keys in action; Let's say you want to create a system that allows anyone to get online and write articles. You would need to keep track of who has written which article so that when the owners of those articles are making changes, they aren't able to make changes to articles that do not belong to them -- same thing applies to deletion. You don't want someone who didn't write an article to be able to delete it.  

Create a table for users ...
```
CREATE TABLE users (
  Name varchar(255),
  Nickname varchar(255),
  Email varchar(255),
  Bio varchar(255),
  id serial
);```  

Using `id serial` we are specifying an auto-incrementing column of this table. Every time a user record is created a row gets added to the database with a unique ID.  

Now let's create a table for articles ...
```
CREATE TABLE articles (
  Title varchar(255),
  Content text,
  id serial,
  user_id integer
);
```




## Data Types in SQL
