# Installing Ruby on Rails

The following "Installing Ruby on Rails" sections are lifted directly from Jordan's [Rails Best Practices](http://www.phantomdata.com/2016/07/21/rails-best-practices.html) guide.

We work in a company with lots of different disciplines all commingling on a regular basis.  PHP, .NET, Java, Rails and Python...  we all get along pretty well.  We're also quite adaptable and end up going where the work is - which might not necessarily be in our favorite discipline.  The most common frustrations I see developers thrown into the Rails world is that of not having started from a good base.

You see, Ruby is pretty popular.  You might not know it, but a metric ton of the critical tools you use daily are built upon it.  For the most part, unless you're running Windows, Ruby is already installed.  ***gasp*** it was that easy?

Not quite.  That version that's installed is probably pretty old.  Not only that, but Ruby's ecosystem is actually pretty complex and diverse.  Over the years we've figured out ways to all work together - but most operating systems don't install Ruby that way.

If you use your system Ruby, you are probably going to have a bad time.  Follow below for steps to obviate that.

## Linux

Linux setup is pretty straight forward.  If you've tried other guides, make sure to examine and clear any remnants from your `~/.bash_profile` and `~/.profile`.

```sh
# Install basic developer tooling
sudo apt-get install build-essential libssl-dev git subversion imagemagick \
  libmagick-dev curl automake libpcre3-dev bison libmysqlclient-dev \
  libxslt-dev libpq-dev libreadline-dev libyaml-dev libcurl4-openssl-dev \
  postgresql postgresql-server-dev-9.1 git nodejs

# Install RVM to properly select Ruby versions
gpg --keyserver hkp://keys.gnupg.net \
  --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
\curl -sSL https://get.rvm.io | bash -s stable

# Install Ruby and Rails (you may have to restart your terminal)
rvm install ruby 2.3.1
rvm use ruby 2.3.1
gem install bundler rails
```

## OSX

OSX setup is also pretty straight forward.  If you've tried other guides, make sure to examine and clear any remnants from your `~/.bash profile` and `~/.profile`.

```sh
# Install Homebrew so you can install other things
/usr/bin/ruby -e \
  "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# Install a database and the most common image library
brew install imagemagick postgresql

# Install RVM to properly select Ruby versions
gpg --keyserver hkp://keys.gnupg.net \
  --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
\curl -sSL https://get.rvm.io | bash -s stable

# Install Ruby and Rails (you may have to restart your terminal)
rvm install ruby 2.3.1
rvm use ruby 2.3.1
gem install bundler rails
```

# An MVC Primer

Ruby on Rails is one of many frameworks that follows the MVC design pattern.  This pattern dictates a distinct separation of concerns between the 3 major components: Model, View and Controller.  Each component represents a layer which a request works its way through as it is serviced.

Rails' concept of MVC dictates that a request is first serviced by a Controller which coordinates various components.  This generally means that a Controller will speak to various Models to gather information and feed it up into a View.

The Model Layer, as described by Rails, is responsible for handling the majority of business logic found within the application.  For the vast majority of CRUD applications, this can be the files found within app/models.  We'll talk about methods for obviating Model Bloat later.

Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of instance variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## Stepping Outside of MVC

MVC is not a silver bullet for every single problem.  It *is* a damned good way to solve common web application architectures but it is often necessary to step outside of these boundaries.  It is a subject of much debate and has no generally agreed upon solution within the Rails community.  Since there is no clear winner, we have simply selected a pattern for you to follow:

1. All domain-specific non-mvc code goes into `app/` - **eg: app/services/cakes_service.rb, app/factories/car_factory.rb, app/whatever**
1. All non-domain-specific non-mvc code goes into `lib/` - **eg: lib/thumbnail_generator.rb, lib/hmac_authenticator.rb, lib/ci_bootstrapper.rb**

The predominant way that you will step out of the MVC pattern is through the usage and implementation of **service classes**.  These classes are typically developed to split out particular *concerns* of a given domain object.  You may find this at odds with Rails Concerns and rightfully so.  Rails Concerns are a hotly debated topic in the Rails community, and as a whole we simply eschew towards using the more agnostic Service Class approach.

You can find an in depth discussion about implementing service classes over on [Stitch Fix's blog](http://multithreaded.stitchfix.com/blog/2015/06/02/anatomy-of-service-objects-in-rails/).

# Rails Clean Code Basics

1. Keep your controllers small - they control things, they don't **do** things
1. Keep your models small - logic that can be cleanly collected into a specific *business concern* should be split out into a *service class*.
1. Run `rubycritic` and `rubocop` to ensure that your code is up to standards
