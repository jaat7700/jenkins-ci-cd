pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Initiating build process'
                git branch: 'main', url: 'https://github.com/jaat7700/jenkins-ci-cd/edit/main/Jenkinsfile'
                echo 'Fetching dependencies...'
                echo 'Compiling React application...'
                echo 'hello my name is Himanshu. hello message'
             }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Executing unit and integration tests'
                echo 'JUnit and Selenium tests are running...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Running static code analysis'
                echo 'Performing SonarQube analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Conducting security assessment'
                echo 'Scanning application using OWASP ZAP...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Initiating deployment to staging'
                echo 'Deploying to AWS EC2 staging server...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Validating staging environment'
                echo 'Executing integration tests on staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Finalizing production deployment'
                echo 'Deploying to AWS EC2 production server...'
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
                $SMTPBody = "The pipeline has been executed successfully."
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "hgmzzgztuyybecfz"  
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "Pipeline execution completed successfully!"
        }

        failure {
            script {
                def powershellCommand = '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 587
                $SMTPFrom = "himanshu4782.be23@chitkara.edu.in"
                $SMTPTo = "himanshu4782.be23@chitkara.edu.in"
                $SMTPSubject = "FAILURE"
                $SMTPBody = "Pipeline encountered errors during execution."
                $SMTPUsername = "himanshu4782.be23@chitkara.edu.in"
                $SMTPPassword = "hgmzzgztuyybecfz" 
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "Pipeline execution encountered failures!"
        }
    }
}
