pipeline {
    agent {
        label 'jenkins-slave' // Replace with the label you have assigned to your pod or agent
    }

    stages {
        stage('Build') {
            steps {
                echo 'Cloning repository...'
                // Use Jenkins 'git' step to clone the repository
                git url: 'https://github.com/sudhvihaan/djangoApp1.git', branch: 'main'
            }
        }
    }

    post {
        always {
            echo 'Sending build info to Jira...'
            jiraSendBuildInfo(
                site: 'devopsfacto.atlassian.net' // Replace with your Jira site name configured in Jenkins
            )
        }
    }
}

