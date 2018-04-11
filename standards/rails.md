# <a href="#rails"></a>Rails Best Practices

## Overview

Ruby on Rails is a framework that follows an MVC design pattern. If you are not familiar with MVC design patterns, check out our [MVC Primer](/standards/rails-mvc.md) for more information.

## Non-MVC Code

Not all code fits perfectly into the MVC pattern. Use the following as a guide when implementing non-MVC code:

1. All domain-specific non-MVC code goes into `app/`. e.g.: `app/services/cakes_service.rb`, `app/factories/car_factory.rb`, `app/whatever`
1. All non-domain-specific non-MVC code goes into `lib/`. e.g.: `lib/thumbnail_generator.rb`, `lib/hmac_authenticator.rb`, `lib/ci_bootstrapper.rb`

For code that falls outside of MVC, prefer to use **service classes** unless there is a compelling reason not to.

### Service Classes

Use the guidelines outlined by [Stitch Fix's blog](http://multithreaded.stitchfix.com/blog/2015/06/02/anatomy-of-service-objects-in-rails/) for implementing service objects. Their recommendations are as follows:

* Do not store state
* Use instance methods, not class methods
* There should be very few public methods
* Method parameters should be value objects, either to be operated on or needed as input
* Methods should return rich result objects and not booleans
* Dependent service objects should be accessible via private methods, and created either in the constructor or lazily

#### Service Class Example

```ruby
# app/services/product_import_service.rb

class ProductImportService

  # Initialize the service with any necessary (or optional) information
  def initialize(connection: nil)
    @connection = connection || Connection.new
  end

  # Use a main public method
  def process
    # Do stuff
  end

  private
  # Additional supporting methods belong here

end
```

## Namespacing

For larger projects it's often beneficial to namespace related models, controllers, and views into sub-folders to help with organization. There are no hard and fast rules but it's helpful to be familiar with how to do it.

For an in-depth discussion on why namespacing is valuable and strategies on how to organize projects, check out [Makandra's blog](https://blog.makandra.com/2014/12/organizing-large-rails-projects-with-namespaces/).

#### Namespacing Example
```
# app/models

/activity
/api
/contact
/invoice
/planner
/report
/project
activity.rb
contact.rb
planner.rb
invoice.rb
project.rb
user.rb
```

## Models

* Keep your models small
* Logic that can be cleanly collected into a specific **business concern** should be split out into a **service class**
  * e.g. `Product.import_products` should be refactored into `ProductImportService`
* Use models for `has_and_belongs_to_many:` relationships, e.g. `has_many: :a_things, through: :a_b_things`
* Namespace related models where it makes sense to do so

## Controllers

* Keep your controllers small - they control things, they don't **do** things
* Use restful routing as much as possible. Avoid non-CRUD actions unless you have a compelling reason

## Front End

The below guidelines are for work done in a team of Rails developers, designed with maintainability and ease of project ramp-up for new Rails people in mind.

When working with a front end developer, talk with them to see what standards and tooling they like to use.

### CSS

* Use SCSS for all your files, including `application.scss`
* Don't use controller-generated asset files
* Keep your CSS modular and component-based
* Use SCSS variables for things like colors, generic padding, and spacing, and keep them in a `_vars.scss` file

A typical folder setup will look something like this:

```
base/
  _elements.scss
  _fonts.scss
  _reset.scss
helpers/
  _utils.scss
  _vars.scss
landmarks/
  _header.scss
  ...
modules/
  _btn.scss
  ...
_screen.scss # loads everything in subfolders
application.scss # loads _screen.scss, and any other applicable stylesheets
```

### Javascript

* Use Javascript, not Coffeescript
* Use Yarn to load Javascript libraries in Rails 5
* Avoid using frameworks with a large learning curve such as React, Angular, etc. unless there is a compelling reason to use it for the project
* Prefer using jQuery where possible
* Like with CSS, keep your Javascript in modular files that make sense for the project structure

A typical folder setup will look something like this:

```
views/
  carouselView.js
  productFormView.js
  ...
application.js # loads main.js, and any other applicable javascript
main.js # loads everything in subfolders, may contain initialization code
```

### Generators

To prevent generating stylesheets and Javascript files for new controllers, add the following to `application.rb`:

```ruby
config.generators do |g|
  g.assets false
end
```

### Views

* Keep business logic and database queries out of views
* Use regular `.erb` in HTML files, not Haml or another templating language
* Use partials responsibly - it's easy to use too many partials, or add too many details and checks into one partial when it should be split into multiple partials.

### Helpers

* Use helpers for display logic, especially if it needs to be used in multiple parts of the site
* Don't use helpers for business logic

## Code Quality

See [Ruby Best Practices](/standards/ruby.md#quality) for recommended tooling and code quality expectations.
