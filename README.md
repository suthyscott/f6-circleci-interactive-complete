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

