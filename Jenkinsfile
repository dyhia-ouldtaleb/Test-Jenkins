pipeline {
  agent any

  tools { nodejs 'NodeJS-18' }

  environment {
    SSH_GITHUB='ssh-github'
    REGISTRY_URL='tonregistry/monapp'
    IMAGE_TAG="${env.BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', credentialsId: SSH_GITHUB, url: 'git@github.com:TON_UTILISATEUR/my-next-app.git'
      }
    }

    stage('Install & Test') {
      steps {
        sh 'npm ci'
        sh 'npm run lint'
        sh 'npm test'
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build -t $REGISTRY_URL:$IMAGE_TAG -f Dockerfile.prod .'
      }
    }

    stage('Push Image') {
      steps {
        withCredentials([usernamePassword(credentialsId:'docker-registry', usernameVariable:'DOCKER_USER', passwordVariable:'DOCKER_PASS')]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin tonregistry'
          sh 'docker push $REGISTRY_URL:$IMAGE_TAG'
        }
      }
    }
  }

  post {
    always { echo 'Pipeline terminé' }
    success { echo '✅ Succès' }
    failure { echo '❌ Échec' }
  }
}
