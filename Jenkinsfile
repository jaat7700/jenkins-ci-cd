pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/jaat7700/jenkins-ci-cd.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'echo Installing dependencies...'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'echo Running tests...'
            }
        }
        stage('Build Project') {
            steps {
                sh 'echo Building project...'
            }
        }
        stage('Deploy (Optional)') {
            steps {
                sh 'echo Deploying project...'
            }
        }
    }
}
