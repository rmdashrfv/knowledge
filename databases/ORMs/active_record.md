# Active Record (Ruby/Rails ORM)

ActiveRecord is an Object Relational Mapping for Ruby applications that provides the developer with a familiar interface to SQL. Put another way, it allows the developer to write Ruby code that will communicate with the database in SQL on the developer's behalf.

## Creating an ActiveRecord Model

A "model" is simply a Ruby class object that inherits from ActiveRecord.  
```
class User < ActiveRecord::Base

end
```  
That's all.  
  
Because this User model inherits from `ActiveRecord::Base`, it now has access to a vast array of useful functions for saving objects, retrieving data, and updating objects. You don't have to write any of this, it's built into ActiveRecord. You also don't have to write an `initialize` method. All of this is handled by ActiveRecord. Here are couple of useful functions that I now have thanks to this ORM:

```
User.new    # create a new instance of user, but doesn't save it
User.all    # returns all saved instances of User
User.find() # returns a user whose ID column matches the number passed in
```  

## Order of Operations

The most basic order of operations with ActiveRecord is as follows:  

```
1) Create a migration file
2) Add a create_table function that specifies columns and data types
3) Migrate new changes to update the database
```  

### 1) Create a migration file
A migration file is a file that specifies a schema for a particular table in your database. There are several ways to create a migration file:  

**Rails**: `rails generate model User name:string email:string age:integer`  
The above command is unique to Ruby on Rails. It will generate a migration file for a User model and automatically include the required code for the columns and data types specified above (located in the `change` function).  

**Sinatra**: `bundle exec rake db:create_migration NAME=create_users`  
The above command is unique to Sinatra apps. It will generate a migration file for a User model, but it will not include the required code for columns and data types in the `change` function.


### 2) Add a create table function that specifies columns and data types
Now that you have a migration, you should run `bundle exec rake db:migrate:status` to get a picture of the current state of your database. The most recently created migration should be listed as `down` in the status column.  

  
For Sinatra applications, you will need to manually add in code to the `change` function for any changes to take place. When we run the `rake db:migrate` command, it will run this `change` function.  

Typically, what you want to do is run the `create_table` function inside of this `change` function. `create_table` specifies the columns and data types this model will use, and these work like the attriubtes of a typical Ruby class, except you don't need to write attr_accessor. Here's an example of a `create_table` function:

```
create_table :users do |t|
  t.string :name
  t.string :email
  t.integer :age
end
```  
  
With that inside of your `change` function, you are now ready to run the following command:  
`bundle exec rake db:migrate`


### 3) Migrate new changes to update the database

Now that you've run `bundle exec rake db:migrate`, run the same command, but with `:status` to see that the last migration that was previously down is now up. Check out your schema file (located at `/db/schema.rb)` and you will see the changes reflected there as well.

---

## I need to change something!

Now that you understand how to get set up, let's go about making changes.   
Let's say your users table is incomplete. You want to update your users table to enable the storage of data for loyalty points. The table itself exists, so you can't simply overwrite the user migration file (and you don't want to).  

This is where rolling back the database comes into play. If you were to run `bundle exec rake db:migrate:status` in the terminal, you would see that your users table is now up because you've migrated the database. Your database schema is like a snapshot of your database's structure at the time you ran your migration files. Once a file has been migrated, it's status is `up`. Therefore, running `bundle exec rake db:migrate` will have no effect, because it only works on migrations whose status is currently `down`.  In addition, simply writing new code into your migration file **will not work**, because in order for you to change the database with the `db:migrate` command, the migration would have to be down. Editing the file while it is up will not work.

To modify the table, here is the order of opertations:

```
1) rollback the latest migration
2) edit a migration file while it is DOWN
3) re-run the migration file to set it back to UP
```

### 1) Rollback the latest migration
First, we rollback the database to a state where the migration file we want to change is `DOWN`.  
`bundle exec rake db:rollback`  
It's very important to note that the table you want to change may not be the most recent table you migrated. So if you have 5 migrations that are up, and you want to change the third migration from the top, you will need to run the rollback command 3 times.

### 2) Edit a migration file while it is DOWN
After step 1 is complete, the migration file is now down. It is now okay to make changes. You can change column names, data types, and default values now. Be sure to save the file once you're done. Using the users table above as an example, I can now do this to my user migration file:  

```
create_table :users do |t|
  t.string :name
  t.string :email
  t.integer :age
  t.date :birthday     # adding a birthday column
  t.boolean :activated # adding a column to detect activation status
end
```

The last two columns (date and birthday) have been added to the Users table, and will now be accessible properties on instances of my User model!
