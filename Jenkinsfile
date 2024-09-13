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
        stage('Parallel Execution') {
            parallel {
                stage('Build 1') {
                    steps {
                        lock('worker_node1') {  // Lock the worker_node1 resource
                            echo 'Cloning repository for Build 1...'
                            hello()   // Call hello() from helloMessage shared library
                            jiraComment body: 'Hello from Jenkins Build 1', issueKey: 'KAN-2'
                            git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
                        }
                    }
                }

                stage('Build 2') {
                    steps {
                        lock('worker_node1') {  // Lock the worker_node1 resource
                            echo 'Cloning repository for Build 2...'
                            hello()   // Call hello() from helloMessage shared library
                            jiraComment body: 'Hello from Jenkins Build 2', issueKey: 'KAN-3'
                            git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
                        }
                    }
                }

                stage('Input 1') {
                    steps {
                        lock('worker_node1') {  // Lock the worker_node1 resource for exclusive access
                            getUser 'Enter response for Input 1', 'Enter response 2 for Input 1'
                        }
                    }
                }

                stage('Input 2') {
                    steps {
                        lock('worker_node1') {  // Lock the worker_node1 resource for exclusive access
                            getUser 'Enter response for Input 2', 'Enter response 2 for Input 2'
                        }
                    }
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

