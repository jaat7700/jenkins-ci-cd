pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/homebrew/Cellar/maven/3.9.9/libexec"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
        EMAIL_RECIPIENT = 'Himanshunain770@gmail.com'
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Fetching source code...'
                sh 'mvn clean package'  
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
            post {
                always {
                    script {
                        def testResult = currentBuild.result ?: 'SUCCESS'
                        emailext subject: "Jenkins Test Stage: ${testResult}",
                                 body: "Test stage completed with result: ${testResult}",
                                 to: env.EMAIL_RECIPIENT
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                sh 'sonar-scanner'  // Ensure SonarQube is configured
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh './dependency-check.sh --project my-app'  // Ensure script is executable
            }
            post {
                always {
                    script {
                        def scanResult = currentBuild.result ?: 'SUCCESS'
                        emailext subject: "Jenkins Security Scan: ${scanResult}",
                                 body: "Security scan completed with result: ${scanResult}",
                                 to: env.EMAIL_RECIPIENT
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
                sh 'curl -X GET http://staging-server/health'
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
                echo 'Deploying to production...'
                sh 'scp target/app.jar user@production-server:/app/'
            }
        }
    }

    post {
        success {
            emailext subject: "Jenkins Pipeline SUCCESS",
                     body: "The pipeline completed successfully!",
                     to: env.EMAIL_RECIPIENT
        }
        failure {
            emailext subject: "Jenkins Pipeline FAILURE",
                     body: "The pipeline failed. Check Jenkins logs for details.",
                     to: env.EMAIL_RECIPIENT
        }
    }
}
