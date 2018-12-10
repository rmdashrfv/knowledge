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
