pipeline {
    agent any

    stages {
        stage('Email Test') {
            steps {
                echo 'Testing Jenkins Gmail SMTP configuration'
            }

            post {
                always {
                    emailext(
                        to: 'mangaraju.arun+jenkins@gmail.com',
                        from: 'mangaraju.arun@gmail.com',
                        replyTo: 'mangaraju.arun@gmail.com',
                        subject: "Jenkins SMTP Test - Build ${env.BUILD_NUMBER}",
                        body: """Hello Sai Arun Mangaraju,

This is a test email from Jenkins.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}

The Jenkins console log is attached.

Regards,
Jenkins
""",
                        attachLog: true,
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }
}
