pipeline {
  agent any

  environment {
    IMAGE_NAME = 'my-next-app'
    CONTAINER_NAME = 'my-next-app-container'
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          bat 'docker build -f Dockerfile.dev -t $IMAGE_NAME .'
        }
      }
    }

    stage('Run Tests') {
      steps {
        script {
          bat 'docker run --rm $IMAGE_NAME npm test'
        }
      }
    }
  }
}
