pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/jaat7700/jenkins-ci-cd.git'
        GIT_BRANCH = 'main'  // Change this if your branch name is different
        EMAIL_RECIPIENT = 'your-email@example.com'  // Change this or use a Jenkins parameter
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo 'Cloning Repository...'
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${GIT_BRANCH}"]],
                        userRemoteConfigs: [[url: GIT_REPO]]
                    ])
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm install'  // Modify if using a different package manager (pip, mvn, etc.)
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                    catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                        sh 'npm test'  // Allows pipeline to continue but marks build as UNSTABLE if tests fail
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing static code analysis...'
                    catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                        sh 'npm run lint'  // Modify based on your analysis tool (ESLint, SonarQube, etc.)
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                        sh 'npm audit'  // Modify based on your security scanner (Snyk, Trivy, etc.)
                    }
                }
            }
        }

        stage('Build Project') {
            steps {
                script {
                    echo 'Building project...'
                    sh 'npm run build'  // Modify based on your project build command
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to Staging...'
                    sh 'chmod +x deploy_staging.sh && ./deploy_staging.sh'  // Ensure script is executable
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to Production...'
                    sh 'chmod +x deploy_production.sh && ./deploy_production.sh'  // Ensure script is executable
                }
            }
        }

        stage('Send Email Notification') {
            steps {
                script {
                    echo 'Sending email notification...'
                    emailext(
                        subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                        body: "Build ${currentBuild.currentResult}: Check console output at ${env.BUILD_URL}",
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the errors.'
        }
    }
}
