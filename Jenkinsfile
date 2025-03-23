pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Fetching the source code from the repository'
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the code and generating artifacts...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                echo 'Running integration tests...'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Checking the quality of the code...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan on the code...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging environment...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment...'
            }
        }

        stage('Approval') {
            steps {
                script {
                    echo 'Pausing for manual approval...'
                    input message: 'Approve deployment to production?', ok: 'Deploy'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production environment...'
            }
        }
    }

    post {
        always {
            emailext (
                to: 'Himanshu4782.be23@chitkara.edu.in',
                subject: "Jenkins Build Notification: ${currentBuild.currentResult}",
                body: """
                <p><strong>Jenkins Pipeline Execution Completed!</strong></p>
                <p>Status: <b>${currentBuild.currentResult}</b></p>
                <p>Check the Jenkins logs for details.</p>
                <p>Build URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html',
                attachLog: true
            )
        }
    }
}
