# Ruby Language Standards

## Formatting

For general Ruby formatting, refer to the excellent community-driven [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide).

## Code Quality

We use [Rubycritic](https://github.com/whitesmith/rubycritic) to lint our projects and check for general code smells. This gem is a wrapper for several other code quality gems including Reek and Rubocop.

Other code quality gems we like to use include:
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
