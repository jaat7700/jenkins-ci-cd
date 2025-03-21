pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/jaat7700/jenkins-ci-cd.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'mvn verify'
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'echo Deploying to Staging...'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'echo Deploying to Production...'
            }
        }
        stage('Send Email Notification') {
            steps {
                mail to: 'your-email@example.com',
                     subject: 'Build Notification',
                     body: "Build Status: ${currentBuild.currentResult}"
            }
        }
    }
}
