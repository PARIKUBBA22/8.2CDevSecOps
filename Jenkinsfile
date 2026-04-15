pipeline {
    agent any

    environment {
        SONAR_SCANNER = 'C:\\sonar-scanner\\sonar-scanner-7.2.0.5079-windows-x64\\bin\\sonar-scanner.bat'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/PARIKUBBA22/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    bat "%SONAR_SCANNER%"
                }
            }
        }
    }
}
