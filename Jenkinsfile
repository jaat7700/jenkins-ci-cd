pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'himanshu4782.be23@chitkara.edu.in'
        USER_EMAIL = 'himanshu4782.be23@chitkara.edu.in'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                sh 'mvn clean package'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Build Stage Completed',
                         body: 'The build stage has completed. Check Jenkins logs for details.'
                }
            }
        }
        // Add your other stages here
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            mail to: "${USER_EMAIL}",
                 subject: 'Pipeline Execution Successful',
                 body: 'The entire pipeline has completed successfully.'
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            mail to: "${USER_EMAIL}",
                 subject: 'Pipeline Execution Failed',
                 body: 'The pipeline has failed. Please check the Jenkins logs for more details.'
        }
    }
}
