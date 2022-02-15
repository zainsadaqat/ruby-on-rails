# Ruby on Rails (MVC Framework)

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
