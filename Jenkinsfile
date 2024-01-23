pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('git pull') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('composer install') {
      steps {
        sh 'composer install'
      }
    }
    stage('env copy') {
      steps {
        sh 'cp .env.example .env'
      }
    }
    stage('key creation') {
      steps {
        sh 'php artisan key:generate'
      }
    }
  }
}