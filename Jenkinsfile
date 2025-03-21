pipeline {
    agent any

    environment {
        PROJECT_TYPE = 'node' // Change this to 'maven' or 'gradle' if needed
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/jaat7700/jenkins-ci-cd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (env.PROJECT_TYPE == 'node') {
                        sh 'npm install'
                    } else if (env.PROJECT_TYPE == 'maven') {
                        sh 'mvn clean install'
                    } else if (env.PROJECT_TYPE == 'gradle') {
                        sh './gradlew build'
                    } else {
                        echo "No valid project type selected."
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    if (env.PROJECT_TYPE == 'node') {
                        sh 'npm test'
                    } else if (env.PROJECT_TYPE == 'maven') {
                        sh 'mvn test'
                    } else if (env.PROJECT_TYPE == 'gradle') {
                        sh './gradlew test'
                    } else {
                        echo "Skipping tests."
                    }
                }
            }
        }

        stage('Build Project') {
            steps {
                script {
                    if (env.PROJECT_TYPE == 'node') {
                        sh 'npm run build'
                    } else if (env.PROJECT_TYPE == 'maven') {
                        sh 'mvn package'
                    } else if (env.PROJECT_TYPE == 'gradle') {
                        sh './gradlew build'
                    } else {
                        echo "Skipping build."
                    }
                }
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { return false } // Change to true if you need deployment
            }
            steps {
                echo 'Deploying application...'
                // Add deployment script here, e.g., SCP to a server or Kubernetes
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check logs for issues.'
        }
    }
}
