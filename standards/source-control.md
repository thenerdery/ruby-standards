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