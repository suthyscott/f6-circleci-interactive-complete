# f6-circleci-interactive-complete

## Setup
Go to GitHub and create a new repo with a README file. 

Go to CircleCI and sign-up/sign-in with GitHub.

Set up a project and use the suggested Hello World config file that circleci will provide. It should look like this:

```
# Use the latest 2.1 version of CircleCI pipeline process engine. See: https://circleci.com/docs/2.0/configuration-reference
version: 2.1
# Use a package of configuration called an orb.
orbs:
  # Declare a dependency on the welcome-orb
  welcome: circleci/welcome-orb@0.4.1
# Orchestrate or schedule a set of jobs
workflows:
  # Name the workflow "welcome"
  welcome:
    # Run the welcome/run job in its own container
    jobs:
      - welcome/run
```

Orbs are packages. Node would be in there if we were using it. 

Workflows are the jobs we want circleci to run for us, like the Procfile in Heroku. 


You should be able to add and commit the config file from circleci. Once you've done that you can go back to GitHub where you'll see a pull request from a new branch named circleci-project-setup. Go ahead and merge that in. 

If you have an issue adding and committing from circleci, you'll need to add the config.yml file manually. Clone your repo down and create a folder called .circleci. Within that folder create a file called config.yml. Go back to circleci.com and follow the steps to copy the config file and then paste it into the confile.yml file you just made locally. Save and push your changes. You should then be able to add the project to circleci.com by telling it to watch that config file. 


Once you have successfully connect the repo and the project in circleci you can look at the welcome/run script that was run. 
 - Spin up environment: created the environment for the repo to run on. It will have info on the server being used, timing etc.... 
 - Preparing environmental variables: it set up a bunch of env variables. 
 - Congratulations! 


### Config.yml

Now we're going to adjust the config.yml file to run what we want it to. 