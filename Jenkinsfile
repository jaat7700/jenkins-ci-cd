pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code'
                echo 'Installing dependencies...'
                echo 'Hello'
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
            script {
                def powershellCommand = '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 587
                $SMTPFrom = "himanshu4782.be23@chitkara.edu.in"
                $SMTPTo = "himanshu4782.be23@chitkara.edu.in"
                $SMTPSubject = "Jenkins pipeline executed successfully!"
                $SMTPBody = "The pipeline executed successfully."
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "phzq pdqk pjxm gvrv"  
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "GREAT SUCCESS!"
        }

        failure {
            script {
                def powershellCommand = '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 587
                $SMTPFrom = "himanshu4782.be23@chitkara.edu.in"
                $SMTPTo = "himanshu4782.be23@chitkara.edu.in"
                $SMTPSubject = "FAILURE"
                $SMTPBody = "Pipeline failed to execute, errors occurred"
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "phzq pdqk pjxm gvrv" 
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "Pipeline Execution Failed!"
        }
    }
}
