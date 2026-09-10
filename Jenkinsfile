pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mangarajuarun-28/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
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
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'SONAR_TOKEN',
                        variable: 'SONAR_TOKEN'
                    )
                ]) {
                    sh '''
                        rm -rf sonar-scanner
                        rm -rf sonar-scanner-*
                        rm -f sonar-scanner.zip

                        curl -L \
                        -o sonar-scanner.zip \
                        https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-8.1.0.6389-linux-aarch64.zip

                        jar xf sonar-scanner.zip

                        mv sonar-scanner-8.1.0.6389-linux-aarch64 sonar-scanner

                        chmod +x sonar-scanner/bin/sonar-scanner

                        sonar-scanner/bin/sonar-scanner
                    '''
                }
            }
        }
    }
}
