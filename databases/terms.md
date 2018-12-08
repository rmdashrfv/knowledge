# Introduction to Databases

A quick introduction to databases. This guide works best if you have a solid understanding of Object-Oriented Programming.

### Database
 A database is an organized collection of information

### Table
A Table is a "section" of a database that holds information about a specific kind of information relating to a single topic. For example: a Users table would hold information about all the users of a website.

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
);```
