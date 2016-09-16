---
layout: page
author: The Nerdery Ruby Standards Task Force
---

# Introduction

Our goal in the creation of this document is to not only improve consistency, but to also allow newer developers joining our discipline to have an easy to use reference point.  Consistency is a key element of software quality and without it all of our efforts eventually turn to spaghetti.

Today at The Nerdery, the Ruby discipline is effectively the Ruby on Rails discipline.  We *do not* do much pure Ruby work and we *do not* do Sinatra work.  Thus, the focus of this document is not actually *Ruby* standards, but instead **Ruby on Rails** standards.

# Contributing

So you want to contribute to this document?  Awesome!  We openly accept collaboration and want your halp!  Please contact @sumpygump for commit access to our [repo on GitHub](https://github.com/thenerdery/ruby-standards)!  You can also open issues over on GitHub and even fork the project to make your own changes before submitting them back to main.

# Further Resources

Remember, this is a standards guide - **not a tutorial**.  If you are interested in learning Ruby then that's fantastic!  Below you'll find a curated list of some of the best resources for getting started:

1. [Nerdery Getting Started Guide]() - for getting started.
1. [Ruby Warrior]() - for learning Ruby.
1. [Rails Best Practices]() - for learning a *right* way.
1. [Blog Tutorial #1]() - Something about this!
1. [Another Blog Tutorial]() - More things.
1. [RailsGuides]() - The ultimate API document for figuring Rails out.

<h1>Table of Contents</h1>

1. TOC
{:toc}

# Ruby Language Standards

The Ruby community as a whole is fairly homogeneous and thoroughly focused on maintaining that community.  As a result, we have an excellent [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) available to us that puts forth most of the usual "how many tabs, how to name methods" sorts of questions.  At The Nerdery, we use this.

We are extremely fortunate in our community to have [Rubocop](https://github.com/bbatsov/rubocop) available to use - which will automatically check for standards violations against the community Ruby Style Guide.  Please make sure that you use **and enforce** this on any of your Ruby projects.

```ruby
  group :development, :test do
    gem 'rubocop'
  end
```

**Follow those standards and you will be set.**

# Installing Ruby

# An MVC Primer

Ruby on Rails is one of many frameworks that follows the MVC design pattern.  This pattern dictates a distinct separation of concerns between the 3 major components: Model, View and Controller.  Each component represents a layer which a request works its way through as it is serviced.

Rails' concept of MVC dictates that a request is first serviced by a Controller which coordinates various components.  This generally means that a Controller will speak to various Models to gather information and feed it up into a View.

The Model Layer, as described by Rails, is responsible for handling the majority of business logic found within the application.  For the vast majority of CRUD applications, this can be the files found within app/models.  We'll talk about methods for obviating Model Bloat later.

Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## Stepping Outside of MVC

# Rails Clean Code Basics

# Source Control Practices

# Testing

# Deployment

# 3rd Party Libraries

## Admin Interfaces

This is a highly subjective choice that should be deeply considered for the given project.  There are roughly 2 modern choices on this subject:

1. [Administrate](https://github.com/thoughtbot/administrate)
1. Custom

Administrate is a useful gem for non-customizable, easy and quick administrative interfaces.  The type of project that this would be useful on is probably the same one that uses Twitter Bootstrap and needs to be done tomorrow.  It falls down heavily when we need to start customizing the administrative back-end to support client demands.

Honestly, writing custom CRUD operations for basic forms is a trivial and relatively fast task.  It is boring and thankless work, but in the end it provides a solid foundation upon which we can make the customizations that most of our clients are looking for in a Rails based project.

## Authentication

Our usual choice for Authentication needs is [Devise](https://github.com/plataformatec/devise).  It is the de-facto standard for the Rails community and carries with it strong community support and high quality documentation.  It is also very easy to customize and skin to our exact needs as defined on a project by project basis.


## Background Jobs

[Delayed::Job](https://github.com/collectiveidea/delayed_job) is our usual choice for a backing engine to support ActiveJob.  It provides solid community support and a strong sharing of knowledge amongst our developers.

## File Uploads and Storage

[Paperclip](https://github.com/thoughtbot/paperclip) is our standard library for handling file uploads and should be your usual choice.  It provides excellent support for local storage as well as storage to S3 via Fog.  Its usage and support is well understood by most Rails developers and carries a high amount of hive-knowledge.

## Pagination

[Kaminari](https://github.com/amatsuda/kaminari) - just use it.

# 3rd Party Services

## Continuous Integration

## File Storage

## Hosting

## Source Control Hosting (SCM)
