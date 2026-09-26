pipeline {
    agent any

    environment {
        APP_NAME = 'test-jenkins'
        ENVIRONMENT = 'dev'
    }

    stages {

        stage('Install') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
                echo "Application: ${APP_NAME}"
                echo "Environment: ${ENVIRONMENT}"
                bat 'python app.py'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m pytest test_app.py'
            }
        }

        stage('Docker Check') {
            steps {
                bat 'docker --version'
                bat 'docker ps'
            }
        }

        stage('Credentials Test') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'practice-secret',
                        variable: 'MY_SECRET'
                    )
                ]) {
                    bat 'echo Credential is available to Jenkins'
                }
            }
        }
    }
}