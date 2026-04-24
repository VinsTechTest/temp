pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t python-cicd-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop python-cicd-container || exit 0'
                bat 'docker rm python-cicd-container || exit 0'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 8087:5000 --name python-cicd-container python-cicd-app'
            }
        }
    }
}