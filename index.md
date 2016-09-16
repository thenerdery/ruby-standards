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

There are really 2 primary ways to handle deployment on Rails projects at The Nerdery:

1. Capistrano
1. Ansible / Chef

Each has their place depending on your current environment.

Capistrano is good for systems which use manually provisioned machines or for which you want to keep the code deployment outside of the server provisioning scripts.  This allows you to deploy code without provisioning everything again. It introduces a number of best practices and is a clear choice over a straight manual deployment.

The other option is using your provisioning scripts to handle your deployments.  This methodology typically involves a git repository that is cloned during your provisioning step and heavily depends upon you treating your new systems as cattle and not pets.  It provides no good long-term maintenance plan for a specific instance, instead assuming that you will kill that instance and spawn a new one when you are doing a deployment.

There are extensive debates and subjective opinions on server provisioning in general.  We have yet to reach a generally accepted consensus, neither at The Nerdery nor the community at large.  Please take the time to have these discussions with knowledgable individuals to determine best fit for your project.

# 3rd Party Libraries

## Admin Interfaces

## Authentication

Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## File Storage

aserkajlhwtaserjskrh  sdrkjthsdrt sdrtgysedrtsdr serldtjOnce a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## Background Jobs

Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## File Storage

aserkajlhwtaserjskrh  sdrkjthsdrt sdrtgysedrtsdr serldtjOnce a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.Once a Controller has gathered enough information from the Model layer - this information is fed up to a View layer by way of class variables (`@cats = Cat.all`).  This view layer is typically a `.erb` file which leverages standard Ruby syntax intermingled with HTML code.

This separation gives us clear choices as to the locations of most items and helps to prevent spaghetti code by having different components talking which have no business knowing about each-other.

## Pagination

## Wizard Processes

# 3rd Party Services

## Continuous Integration

## File Storage

## Hosting

## Source Control Hosting (SCM)
