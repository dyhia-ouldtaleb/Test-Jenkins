pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-next-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -f Dockerfile.dev -t %IMAGE_NAME% .'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'docker run --rm %IMAGE_NAME% npm test'
            }
        }
    }
}
