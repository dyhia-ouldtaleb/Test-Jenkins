pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/dyhia-ouldtaleb/Test-Jenkins.git', branch: 'main'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build('my-next-app')
        }
      }
    }

    stage('Run Tests') {
      steps {
        script {
          docker.image('my-next-app').inside {
            sh 'npm test'
          }
        }
      }
    }
  }
}
