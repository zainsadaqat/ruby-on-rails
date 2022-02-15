# Ruby on Rails (MVC Framework)

what our MVC acronym refers to is the way we direct traffic (with a controller) as it comes in from an external source, looks for data (monitored by the model), and is displayed for the user (through the view).

On [14-feb-2022] I successfully installed rails on MacOS Montery by following these links 1. [GoRails](https://gorails.com/setup/osx/12-monterey#rails) 2. [YouTube](https://www.youtube.com/watch?v=jT_SPPPhRBk&t=202s&ab_channel=ChrisLam) 3. [StackOverflow](https://stackoverflow.com/questions/24736204/rbenv-cant-change-global-ruby-version)

### [Solved] Rails not Installed Error in MacOS Monterey

1. `export PATH="$HOME/.rbenv/bin:$PATH"`

2. `eval "$(rbenv init -)"`

3. `gem install rails`

4. `rbenv rehash`


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

#### Create a new Rails Project with PostgreSQL
`rails new <project_name> -d <database_name>`
