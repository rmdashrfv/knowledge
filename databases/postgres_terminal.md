# Using PostgreSQL in Bash

To access your databases from the terminal, you need to enter the postgres
prompt with the following command:  

`$ sudo -u postgres -i`  

You are now in the postgres prompt. Use the following command to enter postgres:  
`$ psql`  


From here, you can now enter commands specifically for postgres. These commands only work here, not in terminal, or a programming langauge's REPL. In fact, consider this the REPL for PostgreSQL.  

## PostgreSQL commands

```
$ \du # list all user accounts
$ \?  # list all commands
$ \c [DBNAME] # connect to a database
$ \dt # list all tables (when connected to a database)
$ \q # quit postgres
$ \conninfo # connection information

```  

When connected to a database you can run SQL commands.
