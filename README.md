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
```
version: 2.1
orbs:
  node: circleci/node@1.1
jobs: 
  build: 
    executor: 
      name: name/default
      tag: '10.4'
    steps:
      - checkout
      - node/with-cache
      steps: 
        - run npm install
      - run: npm run test
```

Add and commit your changes, then go back to GitHub and refresh to make sure they're there. If you go back to circleci.com you should see that our build job failed. This is because this is not actually a node application and it was not able to complete the npm commands we put in the config.yml. 

Now we're going to adjust the config.yml to run in a docker container, print a message and sleep for a specified amount of time: 
```
version: 2
jobs: #we now have TWO jobs, so that a workflow can coordinate them!
  one: #This is our first job
    docker: #it uses the docker executor
      - image: circleci/ruby:2.4.1 #specifically, a docker iamge with ruby 2.4.1
        auth: 
          username: mydockerhub-user
          password: $DOCKERHUB_PASSWORD # context / project UI env-var reference
    # Steps are a list of commands to run inside the docker container above. 
    steps: 
      - checkout # this pulls code down from GitHub
      - run: echo "A first hello" # This prints "A first hello" to stdout.
      - run: sleep 25 # A command telling the job to "sleep" for 25 seconds. 
  two: # This is our second job. 
    docker: # it runs inside a docker image, the same as above. 
      - image: circleci/ruby:2.4.1
        auth: 
          username: mydockerhub-user
          password: $DOCKERHUB_PASSWORD # context / project UI env-var reference. 
    steps: 
      - checkout
      - run: echo "A more familiar hi" # We run a similar echo command to above. 
      - run: sleep 15 # And then sleep for 15 seconds. 
# Under the workflows: map, we can coordinate our two jobs, defined above. 
workflows: 
  version: 2
  one_and_two: # This is the name of our workflow
    jobs: # And here we tell it what jobs to run.
      - one 
      - two
```


# GitHub branching

We're going to practice branching and merging on GitHub. Go to this repo for instructions on this part of the interactive lecture: https://github.com/suthyscott/f6-individual-branch-practice


