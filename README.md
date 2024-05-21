DevOps task - methoda 

When a git branch is merged into master branch, the job extract the jira issue key from the branch name, and move the jira issue to done.

The repository contains:
1. Jenkinsfile
2. Tests files
3. Two branches for the tests
4. servers directory

The target of the Jenkinsfile:
  when a repository get a pull request to merge to the master branch, the job extract the jira issue from the branch name by the following stages:
  1.  stage 1 - Checkout : 
        Checking out the repository from gitHub.
  2. Extract Branch Name:
       Recognize the commit message of the pull request and extract the branch name from.
  3. Move To Done :
     Connecting to jira site, and locate the issue with the branch name, then move the issue to "done".

The repository use webhook to trig the jenkins job when he recognized pull request.
The Jenkins job and jira linked with credentials and tocken.


Servers:
The servers directory contains more three directories, each contained docker-compose.yml file with specific image and port to the server. To deploy the server you need:
  1. cd to the the specific dicrectory, and run the command : docker compose up.
     
