pipeline {
  agent any
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

  }
}