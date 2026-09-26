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
    }
}
