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

        stage('Docker Build') {
              steps {
                bat 'docker build -t jenkins-python-app:%BUILD_NUMBER% .'
            }
        }
        stage('Docker Push') {
          steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub-creds',
            usernameVariable: 'DOCKER_USERNAME',
            passwordVariable: 'DOCKER_TOKEN'
        )]) {
            bat '''
                echo %DOCKER_TOKEN% | docker login -u %DOCKER_USERNAME% --password-stdin
                docker tag jenkins-python-app:%BUILD_NUMBER% %DOCKER_USERNAME%/jenkins-python-app:%BUILD_NUMBER%
                docker push %DOCKER_USERNAME%/jenkins-python-app:%BUILD_NUMBER%
            '''
        }
    }
}




        stage('Credentials Tests') {
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