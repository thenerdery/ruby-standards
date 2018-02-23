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