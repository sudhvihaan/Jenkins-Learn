@Library(['helloMessage', 'getUser']) _  // Load both libraries together

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
                hello()   // Call hello() from helloMessage shared library
                jiraComment body: 'Hello from Jenkins', issueKey: 'KAN-2'
                git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
            }
        }

        stage('Input') {
            steps {
                getUser 'Enter response 1', 'Enter response 2'  // Call getUser() from getUser shared library
            }
        }
    }

    post {
        always {
            echo 'Sending build info to Jira...'
            jiraSendBuildInfo(
                site: 'devopsfacto.atlassian.net'  // Replace with your Jira site name
            )
        }
    }
}

