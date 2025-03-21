pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'developer@example.com'  // Change this to your email
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Fetching source code...'
                sh 'mvn clean package'  // Modify based on your project
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'  // Modify based on your test framework
            }
            post {
                always {
                    script {
                        def testResult = currentBuild.result ?: 'SUCCESS'
                        emailext subject: "Jenkins Test Stage: ${testResult}",
                                 body: "Test stage completed with result: ${testResult}",
                                 to: EMAIL_RECIPIENT
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                sh 'sonar-scanner'  // Use SonarQube or another tool
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'dependency-check.sh --project my-app'  // Example using OWASP Dependency Check
            }
            post {
                always {
                    script {
                        def scanResult = currentBuild.result ?: 'SUCCESS'
                        emailext subject: "Jenkins Security Scan: ${scanResult}",
                                 body: "Security scan completed with result: ${scanResult}",
                                 to: EMAIL_RECIPIENT
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'scp target/app.jar user@staging-server:/app/'  // Adjust for your setup
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'curl -X GET http://staging-server/health'  // Modify as needed
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
                echo 'Deploying to production...'
                sh 'scp target/app.jar user@production-server:/app/'  // Adjust for production
            }
        }
    }

    post {
        success {
            emailext subject: "Jenkins Pipeline SUCCESS",
                     body: "The pipeline completed successfully!",
                     to: EMAIL_RECIPIENT
        }
        failure {
            emailext subject: "Jenkins Pipeline FAILURE",
                     body: "The pipeline failed. Check Jenkins logs.",
                     to: EMAIL_RECIPIENT
        }
    }
}
