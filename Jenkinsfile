pipeline {
    agent any

    stages {
        stage('Email Test') {
            steps {
                emailext(
                    to: 'mangaraju.arun@gmail.com',
                    from: 'mangaraju.arun@gmail.com',
                    subject: 'Jenkins SMTP Test',
                    body: 'This is a Jenkins Email Extension SMTP test.',
                    attachLog: true
                )
            }
        }
    }
}

The Run Tests stage has completed.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}

The Jenkins build log is attached.

Regards,
Jenkins DevSecOps Pipeline""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        to: 'mangaraju.arun@gmail.com',
                        subject: "Jenkins Security Scan - ${currentBuild.currentResult}",
                        body: """Hello Sai Arun Mangaraju,

The NPM Audit security scan has completed.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: ${currentBuild.currentResult}

The Jenkins build log is attached.

Regards,
Jenkins DevSecOps Pipeline""",
                        attachLog: true
                    )
                }
            }
        }
    }
}
