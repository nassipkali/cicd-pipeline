pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "uralskdev/mybuildimage"
    DOCKER_TAG   = "latest"
  }
  
  stages {
    stage('App Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('App Test') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('Docker Image Build') {
      steps {
        sh 'docker build -t mybuildimage'
      }
    }

    stage('Docker Login') {
      steps {
          withCredentials([usernamePassword(
            credentialsId: 'dockerhub-token',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_TOKEN'
          )]) {
            sh '''
              echo "$DOCKER_TOKEN" | docker login \
                -u "$DOCKER_USER" \
                --password-stdin
            '''
        }
      }
    }
    stage('Docker Push') {
      steps {
        sh """
          docker push ${DOCKER_IMAGE}:${DOCKER_TAG}
        """
      }
    }
  }
}
