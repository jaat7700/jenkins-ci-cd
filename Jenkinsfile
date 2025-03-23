pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Building the application...'
                echo 'Installing dependencies...'
                echo 'Building the React application...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests using JUnit and Selenium'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code using SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan using OWASP ZAP'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying application to AWS EC2 staging server'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on staging environment'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying application to AWS EC2 production server'
            }
        }
    }

    post {
        success {
            withCredentials([string(credentialsId: 'SMTP_PASSWORD', variable: 'SMTP_PASS')]) {
                powershell '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 465
                $SMTPFrom = "himanshu4782.be23@chitkara.edu.in"
                $SMTPTo = "himanshu4782.be23@chitkara.edu.in"
                $SMTPSubject = "Jenkins Pipeline Execution: SUCCESS"
                $SMTPBody = "The Jenkins pipeline has been executed successfully."
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "ijif wmek pkif dmnq"
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object System.Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
            }
            echo "Success Email Sent!"
        }

        failure {
            withCredentials([string(credentialsId: 'SMTP_PASSWORD', variable: 'SMTP_PASS')]) {
                powershell '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 465
                $SMTPFrom = "himanshu4782.be23@chitkara.edu.in"
                $SMTPTo = "himanshu4782.be23@chitkara.edu.in"
                $SMTPSubject = "Jenkins Pipeline Execution: FAILED"
                $SMTPBody = "The Jenkins pipeline has failed. Please check the logs for details."
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "ijif wmek pkif dmnq"
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object System.Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
            }
            echo "Failure Email Sent!"
        }
    }
}
