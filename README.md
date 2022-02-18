# Ruby on Rails

what our MVC acronym refers to is the way we direct traffic (with a controller) as it comes in from an external source, looks for data (monitored by the model), and is displayed for the user (through the view).

### MacOS Default Ruby

```
you should know that macOS comes with a system Ruby pre-installed. 
MacOS Monterey includes Ruby 2.6.8 which is not the newest version. 
If you use the system Ruby you'll need root access (sudo) to install gems (introducing a security risk). 
And you'll end up with a cluster of (sometimes incompatible) gems that can't be easily removed 
to restore your system to a clean state. Please use either asdf, frum, or Homebrew.
```

### Installing ruby with Homebrew
```
If you don't need a version manager, install Ruby using the Homebrew package manager. 
Use this approach if you are only building a casual project that you will not maintain, 
or if you are just trying out Ruby to learn the language. 
You can easily remove Ruby after installing with Homebrew (and re-install a newer version when you need it). 
Don't install Ruby with Homebrew if you need to switch among Ruby versions (use asdf or frum in this case).
```

### asdf, frum, and chruby
```
Asdf and frum are software version managers. Asdf is a good choice because it is a universal version manager 
that installs and manages Ruby, JavaScript, Python, Elixir, and several other languages. Frum is simple and fast, 
working only with Ruby. Chruby works only for Ruby but (unlike Frum) requires installation of a separate installer utility.
```

### rbenv and rvm
```
Rbenv and rvm are also popular as Ruby version managers. Sam Stephenson's rbenv has a more complex implementation 
than frum or chruby (it installs extra “shim” files). RVM was once the most popular of Ruby version managers 
but its additional features (gemsets) are no longer needed and add unnecessary complexity.
```


### What are rvm, rbenv, chruby, and asdf?
```
Asdf, chruby, rbenv, or rvm are software version managers that allow you to switch among Ruby versions 
so you can work on applications that use different versions of Ruby. Asdf manages multiple languages. 
Chruby is the lightest and simplest of Ruby version managers. Rbenv is popular but a little complicated. 
RVM is the oldest Ruby version manager with some extra (and now superfluous) features.
```

### Which is best? rvm vs rbenv vs chruby vs asdf?
```
Version managers such as asdf, chruby, rbenv, or rvm allow you to switch among Ruby versions 
so you can work on applications that use different versions of Ruby. Asdf is good for managing multiple languages. 
Install Ruby with asdf if you are developing Rails web applications (which require Ruby, Node, and Yarn) 
or if you are using multiple languages such as Ruby, Node, and Python. Install Ruby with chruby or rbenv 
if you are just managing Ruby versions (chruby is simpler). Some developers use rvm, 
but rvm has complexity and features that are superfluous with the latest versions of Ruby 
(we longer need to manage gemsets because we have Bundler with Ruby). Some developers use Docker (or Nix) 
for teams with complex project environments (for example, Ruby, Node, Redis, and PostgreSQL 
all in one project) but Docker adds complexity. Finally, simply install Ruby with Homebrew 
if you are building only one project with Ruby (for example, if you are a student learning Ruby).
```

On [14-feb-2022] I successfully installed rails on MacOS Montery by following these links 1. [GoRails](https://gorails.com/setup/osx/12-monterey#rails) 2. [YouTube](https://www.youtube.com/watch?v=jT_SPPPhRBk&t=202s&ab_channel=ChrisLam) 3. [StackOverflow](https://stackoverflow.com/questions/24736204/rbenv-cant-change-global-ruby-version)

### [Solved] Rails not Installed Error in MacOS Monterey

1. `export PATH="$HOME/.rbenv/bin:$PATH"`

2. `eval "$(rbenv init -)"`

3. `gem install rails`

4. `rbenv rehash`

if it still shows again, run the following command in terminal

`\curl -sSL https://get.rvm.io | bash -s stable --rails`

#### Create a new Rails Project with PostgreSQL
`rails new <project_name> -d <database_name>`

`get “pages/home”, to: pages#home”`

#### Rails RESTful Design

`rake routes`

`resources :users`

`resources :users, only: [:index, :new, :create]`

`resources :users, :books, :messages`

### Controller Namespace and Routing

Rails allows you to organize groups of controllers under a namespace with a keyword “namespace” during routing. For instance grouping Articles and Comments Controllers under Admin controller.

```
namespace :admin do 
 resources :articles, :comments
end
```

To get to the articles on your browser you have to prefix it with admin , that is

`/admin/articles`

### Naming Routes

Instead of using raw urls generated by Rails app, Rails allows you to refer to routes by names. For example, the following will create a logout_path or logout_url a named helpers in your application.

`get “sessions/destroy”, as: :logout `

## Rails router

The Rails router is also much simpler than you may originally believe. Ultimately, all we're referring to is the routes.rb file. In this file, all we're doing is telling our app 'when a URL comes in from the browser, send it to this controller action'. It's as simple as that.

### CRUD, Verbs, and Actions

In Rails, a resourceful route provides a mapping between HTTP verbs and URLs to controller actions. By convention, each action also maps to a specific CRUD operation in a database. A single entry in the routing file, such as:

`resources :photos`

creates seven different routes in your application, all mapping to the Photos controller:

<img width="759" alt="Screen Shot 2022-02-16 at 11 13 37 PM" src="https://user-images.githubusercontent.com/83048208/154329220-5c53564d-3762-4845-a217-12a9ea9898b8.png">

### Controller

Controllers do exactly what the name implies: they control. Your controller will be the central hub of all the activity happening in your app. It gathers whatever data you need, applies any necessary logic to that data, and then offers that data to your view. Despite how much controllers do, or maybe because of it, it's best to keep in mind that we want our controller to be as clean and thin as possible.

### Parameters

You will probably want to access data sent in by the user or other parameters in your controller actions. There are two kinds of parameters possible in a web application. The first are parameters that are sent as part of the URL, called query string parameters. The query string is everything after "?" in the URL. The second type of parameter is usually referred to as POST data. This information usually comes from an HTML form which has been filled in by the user. It's called POST data because it can only be sent as part of an HTTP POST request. Rails does not make any distinction between query string parameters and POST parameters, and both are available in the params hash in your controller:

```
class ClientsController < ApplicationController
  # This action uses query string parameters because it gets run
  # by an HTTP GET request, but this does not make any difference
  # to how the parameters are accessed. The URL for
  # this action would look like this to list activated
  # clients: /clients?status=activated
  def index
    if params[:status] == "activated"
      @clients = Client.activated
    else
      @clients = Client.inactivated
    end
  end

  # This action uses POST parameters. They are most likely coming
  # from an HTML form that the user has submitted. The URL for
  # this RESTful request will be "/clients", and the data will be
  # sent as part of the request body.
  def create
    @client = Client.new(params[:client])
    if @client.save
      redirect_to @client
    else
      # This line overrides the default rendering behavior, which
      # would have been to render the "create" view.
      render "new"
    end
  end
end
```

### Generate a Controller in ROR

`rails generate controller <controller_name>`

### Writing request specs

A request spec need not be overly complicated and as you will see, does just what the name implies. By sending a request to a URL we can expect the response to either render a view or redirect us. If your controller action redirects the user, and your request spec follows that redirect, it will ultimately still expect some view to be rendered. That's all it takes. At the end of the day, your request spec just want to make sure that your URL route is rendering the correct view.

