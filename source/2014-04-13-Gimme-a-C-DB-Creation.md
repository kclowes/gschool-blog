---
title: Databases Part 1--Gimme a 'C'! Creating a (very) Simple Task Management App
date: 2014-04-13 22:12 UTC
---

It seems like the more complex things get that we are learning, the more files we have open in our text editor. Which
makes it look super intense, and it also makes it harder to show and tell, so please bear with me. Today I am going to
walk through how to set up a database within Sinatra and do the 'C' in CRUD (Create, Read, Update, Destroy).
This is a tutorial of sorts that assumes that you have a basic feel for Sinatra and the commands
that you need to use it. If you do not, the documentation can be found [here](http://www.sinatrarb.com/intro.html "here"). Also,
this is the abbreviated version of that process that does not get into environment variables which are pretty awesome and
great for security purposes. I highly recommend looking into them if you do not already know.

For the database portion, we have been working with a gem called Sequel, which is awesome and allows us to access our
database easily. So, let's get started. There are a number of different ways to create a PostgreSQL database, but I think
the best way is to make a file, (which I usually call create_database.sql) inside the scripts directory.

![alt text](/images/DB_FileName.png "Database File Name")

In this file, the code that you need to create the database looks as follows:

![alt text](/images/Contents_of_create_db_file.png "Code to Create Database")

We want to make two databases, one for testing, and one for development. Each will have a different URL that begins with
'postgres://'. You can run this file from the command line or you can go into psql and create the database that way too.
Now, you have both your test and development database created!

Next up, we want to make a table within the databases. This gets created in what I usually call the migrations folder. You
can call it whatever you want. The convention within the Migrations folder is to list each migration in order numerically.
So, since this is the first migration, I called it 1. When the script is running, it will be run in numerical order, so
be sure you want them running in the order listed.

![alt text](/images/migrations_file_location.png "Migration File Location")

Inside this file, we have what the actual migration does. Contrary to what the word 'migration' means in normal English,
migration in this case means changes in the skeleton of the database. So, forget about birds while you are doing this,
here and now migration means something completely different. Sequel helps this migration by providing some simple code.
The wording is shown below, and more detailed instructions can be found at: [http://sequel.jeremyevans.net/rdoc/files/doc/migration_rdoc.html].

We want to have both the up and down so that if we start having problems after a migration to we can roll back to the
one before the problems began. The code I used looks like this:

![alt text](/images/migration_script.png "Migration Script")

Then, we need to run the migrations so that the database reflects these changes. From the command line, run:

sequel -m path/to/migrations/folder postgres://host/database

Now, the database is updated with all the structural changes. It is basically the bones of a skeleton that needs organs and muscles and
skin. Let's go ahead and put something into our database. For mine, I decided to make a very simple app. I have an
index page where there is a link to add a new task. The link will take you to a form where you can input a task you need
to do. Then you click submit. The task you put in the form will be posted to the main page. When this post request is
issued, you will call the insert method on the table in your database. The lines of code that I used look like this:

![alt text](/images/posting_to_index.png "Posting to Index")

Hopefully all went well and you now have a database with a table with something in it! When you push
to Heroku, make sure you run the migrations or else you will get some weird errors. From the CLI, when you push to heroku,
run:

heroku run 'sequel -m path/to/migrations/folder postgres://host/database'

And don't forget the quotes! I learned that one the hard way. Now, our 'C' is complete! Good work!

(Pull requests accepted :-)