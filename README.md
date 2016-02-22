# Volt To Do App Tutorial

###Setting Up Volt
1. Make Sure Mongo is installed and running 

 ![alt text](http://i.giphy.com/26FPBjebGHfsXfaIU.gif) 
 ![alt text](http://i.giphy.com/l4KigqBLmJ0eNI4XS.gif)
 * run mongod in terminal after installing it

1. Install the Volt Gem 

 ![alt text](http://i.giphy.com/l4KicLSdzyvBr9Hs4.gif)
 
1. Create a new volt app running the command **volt new application_name**
  * Run bundle update
  * Run bundle exec volt server **do not run this until you know that mongo is running* 
 

***As you update the file, the server will automatically update***


##Building your app
1. Create a view file. ***View files in Volt use .html, not .html.erb)*** 
  * Ours was called todos.html
 
2. In main.html, add a link to page in nav bar 
```HTML
<ul class="nav nav-pills pull-right">
        <:nav href="/">Home</:nav>
        <:nav href="/todos">ToDo</:nav>
        <:user_templates:menu /> 
 ```
3. Add route in the config/routes.rb file 
``` 
client '/todos', action: 'todos'
```

4. Some details to know for your html file:
 * views use section headers i.e. <:Body> and <:Title>, which are capitalized and do not use closing tags
 * anything in {{ and }} are executed server side as ruby, and then sent to view 
 * you can use event bindings to call methods on controller
 ** i.e. e-{eventname}: 

5. Define methods in main_controller. 
 
***Here is an example:***
***In todos.html***
```HTML 
<form e-submit="add_todo" role="form">
        <div class="form-group">
          <label>Todo</label>
          <input class="form-control" type="text" value="{{ _new_todo }}" />
        </div>
      </form> 
 ```
 
***In main_controller.rb***
```Ruby 
def add_todo
      _todos << { name: _new_todo }
      self._new_todo = ''
    end
```

In these two chunks of code, we have an event handler method called 'add_todo'
In this, we have an input box, that takes a value called _new_todo. In our controller, we define the method so that it takes the new_todo and adds it to our array of todos. After that, self._new_todo resets the input box to be empty. 



### Docs for referencing 

[Mongo Docs](https://docs.mongodb.org/manual/installation/)

A full step by step tutorial can be found in the [Volt Docs](http://docs.voltframework.com/en/tutorial/a_sample_todo_app.html) 
