@Library('helloMessage') _   // Load the helloMessage shared library
@Library('getUser') _        // Load the getUser shared library

properties([
    pipelineTriggers([
        upstream(
            threshold: hudson.model.Result.SUCCESS,
            upstreamProjects: 'Job1-to-trigger-another-job'
        )
    ])
])

pipeline {
    agent {
        label 'jenkins-slave' // Replace with your agent label
    }

    stages {

        stage('Build') {
            steps {
                echo 'Cloning repository...'
                // Call the hello() function from the helloMessage shared library
                hello()
                jiraComment body: 'Hello from Jenkins', issueKey: 'KAN-2'

                // Use Jenkins 'git' step to clone the repository
                git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
            }
        }

        stage('Input') {
            steps {
                // Call the getUser function from the getUser shared library
                getUser 'Enter response 1','Enter response 2'
            }
        }
    }

    post {
        always {
            echo 'Sending build info to Jira...'
            jiraSendBuildInfo(
                site: 'devopsfacto.atlassian.net' // Replace with your Jira site name
            )
        }
    }
}

