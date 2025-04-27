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
                sh 'mvn clean package'  // Example build tool
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Build Stage Completed',
                         body: 'The build stage (using Maven) has completed. Artifacts are generated. Check Jenkins logs for details.'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using Maven Surefire Plugin...'
                sh 'mvn test'  // Running unit and integration tests
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'  // Publish test reports
                    mail to: "${USER_EMAIL}",
                         subject: 'Unit and Integration Tests Completed',
                         body: 'Unit and integration tests executed. Test reports generated. Check Jenkins logs for details.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis using SonarQube...'
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Code Analysis Completed',
                         body: 'Static code analysis using SonarQube is done. Check SonarQube dashboard and Jenkins logs for details.'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency-Check...'
                sh 'dependency-check.sh --project "MyApp" --scan ./'
            }
            post {
                always {
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                    mail to: "${USER_EMAIL}",
                         subject: 'Security Scan Completed',
                         body: 'Security scan using OWASP Dependency-Check completed. Check reports and Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying build artifacts to Staging environment using SCP...'
                sh 'scp target/*.jar user@staging-server:/opt/staging-app/'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Staging Completed',
                         body: 'Build artifacts deployed to the Staging server. Check Jenkins logs and Staging server for verification.'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests against the Staging environment using Postman/Newman...'
                sh 'newman run integration-tests.postman_collection.json --environment staging.postman_environment.json'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Integration Tests on Staging Completed',
                         body: 'Integration tests against Staging environment completed. Check Newman test results and Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying artifacts to Production server using SCP...'
                sh 'scp target/*.jar user@production-server:/opt/prod-app/'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Production Completed',
                         body: 'Production deployment completed successfully. Validate production system and check Jenkins logs for confirmation.'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            mail to: "${USER_EMAIL}",
                 subject: 'Pipeline Execution Successful',
                 body: 'The entire pipeline has completed successfully. Production environment is updated.'
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            mail to: "${USER_EMAIL}",
                 subject: 'Pipeline Execution Failed',
                 body: 'The pipeline has failed. Please check the Jenkins logs and failed stage for investigation.'
        }
    }
}
