pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'git pull'
                 git clone "https://github.com/sudhvihaan/djangoApp1.git"
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
