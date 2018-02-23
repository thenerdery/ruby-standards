# <a href="#ruby"></a>Ruby Best Practices

## Formatting

For general Ruby formatting, refer to the excellent community-driven [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide).

## <a href="#quality"></a>Code Quality

Use [Rubycritic](https://github.com/whitesmith/rubycritic) to lint projects and check for general code smells. This gem is a wrapper for several other code quality gems including Reek and Rubocop.

Other useful code quality gems include:
* [Brakeman](https://github.com/presidentbeef/brakeman)
* [Bullet](https://github.com/flyerhzm/bullet)
* [SimpleCov](https://github.com/colszowka/simplecov)

```ruby
group :development do
  gem 'brakeman', require: false
  gem 'bullet', require: false
  gem 'rubycritic', require: false
end

group :test do
  gem 'simplecov', require: false
end
```

<!-- TODO: When to ignore Rubycritic / how to use it sanely -->

<!-- TODO: Typical Rubycritic configuration? -->

## Debugging & Development Errors

Use [Better Errors](https://github.com/charliesome/better_errors) for quick access to a console on development runtime errors, and [Byebug](https://github.com/deivid-rodriguez/byebug) for line-by-line debugging.

```ruby
group :development do
  # Access an IRB console on exception pages or by using <%= console %> anywhere in the code.
  gem 'better_errors'
  gem 'binding_of_caller'
end

group :development, :test do
  gem 'byebug'
end
```