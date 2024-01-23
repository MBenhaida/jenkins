pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        sh 'echo building...'
      }
    }
  }
  post {
    always {
      sh 'echo building completed...'
    }
  }
}