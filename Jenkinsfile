pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    IMAGE_NAME = 'marouane/jenkins-exam-laravel'
    IMAGE_TAG = 'latest'
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
      }
    }
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