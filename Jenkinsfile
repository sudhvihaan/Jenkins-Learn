
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add actual build commands here, e.g., 'sh "make build"' or any other build commands.
            }
        }
    }

    post {
        always {
            echo 'Sending build info to Jira...'
            jiraSendBuildInfo (
                site: 'JIRA_SITE_NAME' // Replace with your Jira site name configured in Jenkins
            )
        }
    }
}
