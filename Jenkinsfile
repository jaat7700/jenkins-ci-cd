pipeline {
    agent any

    environment {
        SMTP_SERVER = 'smtp.gmail.com'
        SMTP_PORT = 587
        SMTP_USERNAME = credentials('himanshu4782.be23@chitkara.edu.in')  // Jenkins credentials for the Gmail username
        SMTP_PASSWORD = credentials('hgmz zgzt uyyb ecfz')  // Jenkins credentials for the Gmail password
        SMTP_FROM = 'himanshu4782.be23@chitkara.edu.in'
        SMTP_TO = 'himanshu4782.be23@chitkara.edu.in'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Initiating build process'
                git branch: 'main', url: 'https://github.com/jaat7700/jenkins-ci-cd.git'  // Cloning the repository
                echo 'Fetching dependencies...'
                echo 'Compiling application...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Executing unit and integration tests'
                echo 'Running JUnit and Selenium tests...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Running static code analysis'
                echo 'Performing SonarQube analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Conducting security assessment'
                echo 'Scanning application using OWASP ZAP...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Initiating deployment to staging'
                echo 'Deploying to AWS EC2 staging server...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Validating staging environment'
                echo 'Executing integration tests on staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Finalizing production deployment'
                echo 'Deploying to AWS EC2 production server...'
            }
        }
    }

    post {
        success {
            script {
                def emailBody = '''
                    The Jenkins pipeline executed successfully. All stages completed without errors.
                '''
                sendEmail('Jenkins Pipeline Execution Successful', emailBody)
            }
            echo "Pipeline execution completed successfully!"
        }

        failure {
            script {
                def emailBody = '''
                    The Jenkins pipeline encountered errors during execution. Please check the logs for details.
                '''
                sendEmail('Jenkins Pipeline Failed', emailBody)
            }
            echo "Pipeline execution encountered failures!"
        }
    }
}

// Send email function to avoid repetition (using Shell)
def sendEmail(subject, body) {
    sh """
        echo "$body" | mail -s "$subject" "$SMTP_TO" -r "$SMTP_FROM" -S smtp="$SMTP_SERVER:$SMTP_PORT" \
            -S smtp-auth=login -S smtp-auth-user="$SMTP_USERNAME" -S smtp-auth-password="$SMTP_PASSWORD" \
            -S ssl-verify=ignore
    """
}
