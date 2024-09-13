@Library('MySharedLibrary') _

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
        label 'jenkins-slave' // This is the agent used for the pipeline
    }

    stages {

        stage('Build') {
            steps {
                lock('worker_node1') {  // Lock the worker_node1 resource
                    echo 'Cloning repository...'
                    hello()   // Call hello() from helloMessage shared library
                    jiraComment body: 'Hello from Jenkins', issueKey: 'KAN-2'
                    git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
                }
            }
        }

        stage('Input') {
            steps {
                lock('worker_node1') {  // Lock the worker_node1 resource for exclusive access
                    getUser 'Enter response 1', 'Enter response 2'  // Call getUser() from getUser shared library
                }
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

