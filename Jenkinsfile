pipeline {
    agent any
        environment {
        //environment var for my jira site
        JIRA_SITE = 'liavdarzi'
    }
    stages {
        stage('Checkout') {
            steps {
                //checkout the repo from github
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url:'https://github.com/liavdarzi/methoda_repo_final.git']])
            }
        }
        stage('Extract Branch Name') {
            steps {
                script {
                    //find the last pull request to merge
                    def commitMessage = bat(script:'git log -1', returnStdout: true).trim()
                    def branchNameMatcher = commitMessage =~ /Merge pull request #\d+ from .+\/(.+)/ 
                    def branchName = branchNameMatcher ? branchNameMatcher[0][1] : 'Unknown'
                    //extract the branch name, define him as a evr var and print him
                    echo "Branch Name: ${branchName}"
                    env.BRANCH_NAME = branchName
                }
            }
        }
        stage('Move To Done'){
            steps{
                script{
                    //make sure that the branch name is in a key form
                    if (env.BRANCH_NAME != 'Unknown'){
                    withEnv(["JIRA_SITE=${env.JIRA_SITE}"]) {
                    def issue_key = env.BRANCH_NAME
                    def result = jiraGetIssue idOrKey: issue_key, failOnError:false

                    // status change
                    def transition_to_closed_jira_id = 31 // you need to find out your ID
                    def transitionInput = [ transition: [ id: transition_to_closed_jira_id ] ]
                    jiraTransitionIssue idOrKey: issue_key, input: transitionInput
                    }
                    }
                }
            }
        }
    }
}

        
        
