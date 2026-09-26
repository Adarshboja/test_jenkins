pipeline {
    agent any

    stages {

        stage('Install') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Build') {
            steps {
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