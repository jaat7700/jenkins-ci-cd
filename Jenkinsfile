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
                // Run Maven build command if needed, adjust for your project
                // sh 'mvn clean package'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Build Stage Completed',
                         body: 'The build stage has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Run your tests here (e.g., using Maven, Gradle, or a testing framework)
                // sh 'mvn test'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Unit and Integration Tests Completed',
                         body: 'The unit and integration tests have completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                // Use a tool like SonarQube for code analysis (if configured)
                // sh 'mvn sonar:sonar'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Code Analysis Completed',
                         body: 'The code analysis stage has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // If using tools like OWASP Dependency-Check or similar, add the command here
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Security Scan Completed',
                         body: 'The security scan has completed. Check the Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Add deployment steps for your staging environment (e.g., Docker, Kubernetes, etc.)
                // sh './deploy_staging.sh'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Staging Completed',
                         body: 'Deployment to the staging environment has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Run tests in the staging environment
                // sh 'mvn verify'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Integration Tests on Staging Completed',
                         body: 'Integration tests on staging have completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Add deployment steps for your production environment
                // sh './deploy_production.sh'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Production Completed',
                         body: 'Deployment to production has completed. Check Jenkins logs for details.'
                }
            }
        }
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
