---
title: Databases Part 2--Gimme an 'R-U-D'! Completing CRUD with Sinatra and Sequel
date: 2014-04-19 22:12 UTC
---


Week 7 at gSchool completed. All I can say is wow... it has gone by so fast. Anyway, today I am going to continue to work
through the read, update and destroy steps of databasing. Since last week we went through the create, (which is really the most
difficult part I think), the rest is relatively simple. Reading a database is querying it based on your
specifications. Of course, our tasks can be 'read' on the homepage where we have displayed them. Let's make it slightly more difficult
by reading them one by one. First, we need to add a 'Show Tasks' link. I had it link to the '/task/:id' endpoint. In the
 index.erb file, I have the tasks table converted to an array of hashes in order for me to iterate through it. The array
looks something like this: [{:id => 'id', :task => 'task 1'}]. I am pretty sure there is a better way to do this, but this works.
As you can see from the code below, I have each task from the array displayed in list form. I took the id from the hash
as well in order to use it for the URL link. The snippet of code from index.erb that I used for this purpose is shown below:


```
<ul>
  <% tasks_array.each do |hash| %>
    <li>
      <%= hash[:task] %>
      <% id = hash[:id] %>
      <a href="/task/<%= id %>">Show task </a>
    </li>
  <% end %>
</ul>
```

Then, in the app.rb folder, when a get request is issued to '/task/:id' I made a new erb file called show_task that will
show each task individually. A user can edit (update) or delete a task from this view. A link is provided to edit the task and
to delete the task. When the 'edit task' link is clicked, a get request is issued to the edit_task.erb view, and the user
fills in a form with what they would like to update that particular task to. When the button is clicked to submit the
changes, the app will take the id from the URL, and update the item id in the database. The code in the app looks like this:

```
  get '/task/:id/edit' do
    erb :edit_task, :locals => {:id => params[:id]}
  end
```
```
  put '/task/:id' do
    id = params[:id].to_i
    tasks_table.update({:id => id, :task => params[:edited_task]})
    redirect '/'
  end
```

This gets a little tricky in Sinatra, so you have to put a special line in the HTML form as shown below:

```
<form action="/task/<%= id %>" method="post">
  <input type="hidden" name="_method" value="put">
  <input type="text" name="edited_task">
  <button type="submit">Submit</button>
</form>
```

This should all look familiar except for the second line. You have to do some gymnastics to get the 'put' to work, but
that second line is all you have to do. An awesome blog post by Mike Ebert can be found [here](http://www.sinatrarb.com/intro.html "here").
He explains it much better than I can.

To update that particular item, we will use the id to find it, and the sequel command 'update' to edit that item. In the
app file the code looks like this:

```
  put '/task/:id' do
    id = params[:id]
    tasks_table.where(:id => id).update({:task => params[:edited_task]})
    redirect '/'
  end
```

The only thing left to do now is delete!

Deleting is easy. All you have to do is add a delete button (via a form), and the code in the application looks like this:

```
  delete '/task/:id' do
    id = params[:id]
    tasks_table.where(:id => id).delete
    redirect '/'
  end
```

The delete button is similar to the update in that we have to do some trickery. To delete in the form, the line you need
looks like this:

```
<form action="/task/<%= id %>" method="post">
  <input type="hidden" name="_method" value="delete">
  <button type="submit">Delete Task</button>
</form>
```

Disclaimer to anyone looking at this post and the last:

I am almost certain that there are better, more efficient ways to do everything that I have just done in this blog post.
I am also pretty certain that I will look back on this post someday and cringe. That being said, these two posts are
about me writing shitty code before I can write (while learning to write) pretty code. Thanks for bearing with me!

