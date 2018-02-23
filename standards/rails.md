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

#### Example Service Class

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

## Clean Code Basics

1. Keep your controllers small - they control things, they don't **do** things
1. Keep your models small - logic that can be cleanly collected into a specific *business concern* should be split out into a *service class*.
1. Run `rubycritic` and `rubocop` to ensure that your code is up to standards
