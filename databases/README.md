# Databases

Learn how information is stored and persisted with SQL using the SQLite3 and PostgreSQL databases.


### What is SQLite3?

SQLite3 is a file-based database. All the data is written to a `.sqlite` file. SQLite is not recommended for production applications due to the fact that only a single user can write to the file at a time which means it doesn't scale well at all (of course, this does depend on how much the application is even using the database).  

But don't write SQLite3 off too quickly. This light database actually works well for systems that have no need for administrators; things like televisions, games, drones, and thermostats. Because SQLite3 is so easy to set up on any platform, it's also a great choice for when you want to dive right into SQL.
