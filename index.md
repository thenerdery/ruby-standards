# Ruby Language Standards

The Ruby community as a whole is fairly homogeneous and thoroughly focused on maintaining that community.  As a result, we have an excellent [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) available to us that puts forth most of the usual "how many tabs, how to name methods" sorts of questions.  At The Nerdery, we use this.

We are extremely fortunate in our community to have [Rubocop](https://github.com/bbatsov/rubocop) available to use - which will automatically check for standards violations against the community Ruby Style Guide.  Please make sure that you use **and enforce** this on any of your Ruby projects.

```ruby
  group :development, :test do
    gem 'rubocop'
  end
```

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

# Source Control Practices

## Hosting

There are 2 primary means for hosting source control on Nerdery Rails projects:

1. GitHub
1. Self-hosted Nerdery BitBucket

GitHub is our usual go-to for source control hosting as it provides the highest level of 3rd party service integration.  This level of service allows for easy integration with 3rd party tools like CircleCI, CodeClimate and Heroku.

Our internally self-hosted Nerdery BitBucket service provides a bare-bones code hosting solution that is useful when a client does not wish to pay any additional fees.  It lacks 3rd party support for our typical tools (such as CircleCI, Code Climate and Gemnasium), so you will need to budget in additional time (40-80hours) for integration with our internal CI server Bamboo.

## Branching Strategies

We firmly believe that branching strategies should be appropriate for the particular project and team-type associated.  The most important thing, when it comes to branching strategies, is clear communication and consistent amongst a given project.  As such, including a **contributing** section within the `README.md` is best practice and strongly encouraged.

An example of such a section from a recent project (2016/09/16) is as such:

> **Contributing**
>
> This project is leveraging *Pull Requests* for handling code management.  For each **feature** that you are looking to build, create a branch off of `develop` with the format of `feature/my-feature`.  Once complete, make a Pull Request and a lead should review your request and merge it into develop once complete.
>
> Before making a PR, ensure that you have merged develop back into your branch and that all tests & rubocops are passing.  Your PR will not be merged in if these conditions are not met.
>
> For **emergency fixes**, branch off of `master` to make your fix.  Once tested and complete, merge this branch back into master and then develop.

If a branching strategy has not been specified for a project, consider the [git-flow](http://danielkummer.github.io/git-flow-cheatsheet/) approach as a good starting point.


# Deployment

There are really 2 primary ways to handle deployment on Rails projects at The Nerdery:

1. Capistrano
1. Ansible / Chef

Each has their place depending on your current environment.

Capistrano is good for systems which use manually provisioned machines or for which you want to keep the code deployment outside of the server provisioning scripts.  This allows you to deploy code without provisioning everything again. It introduces a number of best practices and is a clear choice over a straight manual deployment.

The other option is using your provisioning scripts to handle your deployments.  This methodology typically involves a git repository that is cloned during your provisioning step and heavily depends upon you treating your new systems as cattle and not pets.  It provides no good long-term maintenance plan for a specific instance, instead assuming that you will kill that instance and spawn a new one when you are doing a deployment.

There are extensive debates and subjective opinions on server provisioning in general.  We have yet to reach a generally accepted consensus, neither at The Nerdery nor the community at large.  Please take the time to have these discussions with knowledgeable individuals to determine best fit for your project.

# 3rd Party Libraries

## Admin Interfaces

This is a highly subjective choice that should be deeply considered for the given project.  There are roughly 2 modern choices on this subject:

1. [Administrate](https://github.com/thoughtbot/administrate)
1. Custom

Administrate is a useful gem for non-customizable, easy and quick administrative interfaces.  The type of project that this would be useful on is probably the same one that uses Twitter Bootstrap and needs to be done tomorrow.  It falls down heavily when we need to start customizing the administrative back-end to support client demands.

Honestly, writing custom CRUD operations for basic forms is a trivial and relatively fast task.  It is boring and thankless work, but in the end it provides a solid foundation upon which we can make the customizations that most of our clients are looking for in a Rails based project.

*Please note*, ActiveAdmin purposefully does not show up in this list because they have been slow to keep up with major versions of Rails.  Even as of this writing, Rails 5 support is present only in master and is listed as "preliminary".

## Authentication

Our usual choice for Authentication needs is [Devise](https://github.com/plataformatec/devise).  It is the de-facto standard for the Rails community and carries with it strong community support and high quality documentation.  It is also very easy to customize and skin to our exact needs as defined on a project by project basis.


Our typical setup procedure for devise looks something like:

```sh
$ rails generate devise:install
$ rails generate devise User
$ rails generate devise:views
```

For the most part, any deviations from Devise's standard functionality is a result of custom needs on a project.  Devise has excellent documentation on their GitHub page and can easily be extended to support most of our needs.

If you find yourself repeatedly doing something, please don't hesitate to open an issue so that we can document it here.

## Background Jobs

Background Job runners are a fairly cut-and-dry bunch without too many differentiators.  Our developer have the most experience with [Delayed::Job](https://github.com/collectiveidea/delayed_job), so that is what we'll usually expect to find on a given project.

If you find one that you *really* like and feel is way superior, please open an issue or a PR so that we can have a discussion about it.

## File Uploads and Storage

[Carrierwave](https://github.com/carrierwaveuploader/carrierwave) is another choice we often use.  It provides all the same support for storage (thanks to Fog).  One main difference, between it and Paperclip, is its ability to [cache a file after upload so it does not require uploading again after an invalid form submission](https://github.com/carrierwaveuploader/carrierwave#making-uploads-work-across-form-redisplays).  Our primary recommendation is to use CarrierWave.

[Paperclip](https://github.com/thoughtbot/paperclip) is a good choice for handling file uploads and storage.  It provides excellent support for local storage as well as storage to S3 via Fog.  Its usage and support is well understood by most Rails developers and carries a high amount of hive-knowledge.

## Pagination

[Kaminari](https://github.com/amatsuda/kaminari) - just use it.

# 3rd Party Services

Our standard package of 3rd party services includes the following:

1. AWS for Application Hosting
1. GitHub for Code Hosting
1. CircleCI for Continuous Integration / Deployment

Since GitHub and CircleCI are discussed above, the rest of this section will deal specifically with AWS.

There are many hosting providers that provide a variety of costs, but AWS provides the simplest and cleanest growth path of any provider.  It easily and cost-effectively allows us to scale from a small single-server application to a load balanced multi-tiered SoA style app while still maintaining a continuity of service.

Our typical usages of AWS include:

1. EC2 instances for hosting applications
1. RDS instances for hosting databases
1. S3 for hosting uploaded files
1. ElastiCache instances for hosting in-memory data stores
1. OpsWorks for provisioning each if the size or complexity is large

# Documentation

Good documentation makes a long-lived project easier to understand and maintain. It can help introduce new developers to an unfamiliar codebase, or serve as a reference point for the team coming back to code 6 months later. Documentation may also cover important architectural decisions, complex business logic, or quirks and workarounds of the tech we're working with. Just as we put effort into making tests that last to ensure our application is stable and robust, we also focus on providing meaningful documentation.

A great article on improving Rails-based documentation published by Aaron Sumner can be found here. Many of the practices described below are pulled from his philosophy.

## Start with the README
Your application’s README is still its gateway, the first thing new developers will likely read when they access its source code. If your app’s README consists of the default given to every new Rails app, it’s time to change it.

Your README should include:

* A brief description of what the application does.
* How to install dependencies, especially those that are more complex than a simple `bundle install`. For example, if I need to to install Redis or ImageMagick to work on the app, or configure environment variables to talk to external services, let me know up front.
* How to run the application’s test suite, to verify that setup was successful. Again, note special external dependencies, like PhantomJS.
* How to generate the docs, to get to a more detailed description of the application’s code.

## Remove generated documentation from source control

The HTML version of your Rails docs will need to be regenerated regularly, in order to keep up with the code they explain. Ignoring the doc/app directory makes sure that stale documentation doesn't stick around from commit to commit, and just makes commits cleaner in general. This is why it’s important to mention how to generate the docs in your README as they won’t be easily accessible, otherwise.

## Write clear documentation

* __Don't assume knowledge of the business__: If you've been working in the application for awhile, the names you've given your classes and methods may seem obvious, but to a newcomer they can be a large hurdle to overcome. Help explain ___why___ things are called what they are.
* __Do assume knowledge of Rails__: The rule of thumb is to document ___why___, now ___how___. Document under the assumption that the reader can read Ruby code, or at least knows how to search Google or Stack Overflow to learn more about specific methods.

## YARD + RDOC

We recommend utilizing the [YARD gem](http://yardoc.org/) in conjunction with the standard [RDOC documentation system](http://rdoc.sourceforge.net/doc/) to provide clear and consistent documentation on our projects. YARD fills in some of the gaps that RDOC does not address by allowing us to organize our codes meta and behavioural data through the use of [tags](http://www.rubydoc.info/gems/yard/file/docs/Tags.md). Not only does this create consistency between our projects, but it also more closely represents the way documentation blocks are handled via the other disciplines at The Nerdery, making point of entry into the language easier for an outside developer to understand.

### The `.yardopts` file

YARD accepts [many different options](http://www.rubydoc.info/gems/yard/YARD/CLI/Yardoc), and for ease of development it is recommended that you use a `.yardopts` file to outline these options. YARD will automatically parse this file every time `yard` is run and conform to it's requests. A recommended starter file is outlined below

    --private
    --markup=markdown
    app/**/*.rb -
    lib/**/*.rb -
    
This starter file tells YARD to document all private methods, interpret and render markup in the docblocks, and generate documenation for all *.rb files located in the app and lib folders. 

### Markdown format

YARD supports [multiple formats](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Which_Markup_Format_) for it's markup rendering. Due to the industry wide acceptance and use of standard Markdown for most circumstances we recommends utilizing `markdown` as the format of choice on our Ruby projects.

### Do's & Dont's

[YARD](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md) and [RDOC](http://rdoc.sourceforge.net/doc/) are very extensive. We encourage you to read over the documentation and explore the vast amount of options available to you, however documenting too much, or using unwise practices can make your documentation just as bad as not having any at all. In this section we'll cover our recommended practices while using this documentation engine combination:

#### __DO__ 
* Provide a documentation block at the top of every class file. This should contain:
    * A description of the classes function (___why___ not ___how___) within the application.
    * Your [author name](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#author).
    * A [version number](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#since) of when the class was first added to the project. 
* Provide a documentation block at the top of every method with the exception of standard CRUD controller operations (`index`|`new`|`create`|`show`|`edit`|`update`|`destroy`). This should contain:
    * A description of the methods function (___why___ not ___how___) within the class.
    * All [paramaters](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#param) of the method.
    * All [options](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#option) if an options Hash is being used as a param.
    * A [return](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#return) value. If no return value is produced by the method `void` would be the expected return.
* Document all [model attributes](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Documenting_Attributes). Obviously this means writing each to their own line and not strining them together via commas. In the event you need separate documenation for the attributes getter and setter then follow [these steps]( http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Documentation_for_a_Separate_Attribute_Writer).
* Use [Duck-Type specifiers](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#Duck-Types) when appropriately.
    
#### __DON'T__
* Use YARD based [reference tags](http://www.rubydoc.info/gems/yard/file/docs/GettingStarted.md#Reference_Tags). Although this methodology reduces DRY documentation it also enforces coupling.
* Overload your documentation. Having overly cumbersome documentation is just as bad as having no documentation at all. Keep your docblocks small, concise, and to the point. Often throughout the RubyDocs and YARD documentation pages you will be presented with large docblocks filled with markdown and html structures, unless this type of documentation adds significant understandability to the class or method we ask that you refrain from emulating this. "Short, Sweet, To The Point"
* Don't create [custom tags](http://www.rubydoc.info/gems/yard/file/docs/Tags.md#Adding_Custom_Tags) unless absolutely vital to the understandability of the documentation. If you are presented with a case where you do need to make them ensure that you are always namespacing them.