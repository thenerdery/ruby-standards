# Deployment

There are really 2 primary ways to handle deployment on Rails projects at The Nerdery:

1. Capistrano
1. Ansible / Chef

Each has their place depending on your current environment.

Capistrano is good for systems which use manually provisioned machines or for which you want to keep the code deployment outside of the server provisioning scripts.  This allows you to deploy code without provisioning everything again. It introduces a number of best practices and is a clear choice over a straight manual deployment.

The other option is using your provisioning scripts to handle your deployments.  This methodology typically involves a git repository that is cloned during your provisioning step and heavily depends upon you treating your new systems as cattle and not pets.  It provides no good long-term maintenance plan for a specific instance, instead assuming that you will kill that instance and spawn a new one when you are doing a deployment.

There are extensive debates and subjective opinions on server provisioning in general.  We have yet to reach a generally accepted consensus, neither at The Nerdery nor the community at large.  Please take the time to have these discussions with knowledgeable individuals to determine best fit for your project.