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
    stage('git pull') {
      steps {
        sh 'git pull origin main'
      }
    }
    stage('docker build') {
      steps {
        sh 'apt-get update'
        sh 'apt-get install -y docker.io'
        sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
      }
    }
    stage('composer install') {
      steps {
        sh 'composer install'
      }
    }
    stage('env setup') {
      steps {
        script {
          if (!fileExists('.env')) {
            sh 'cp .env.example .env'
            sh 'php artisan key:generate'
          } else {
            echo '.env file already exists. Skipping env setup.'
          }
        }
      }
    }
    stage('running migrations and seeders') {
      steps {
        sh 'php artisan migrate --seed'
      }
    }
    stage('launching the app') {
      steps {
        sh 'php artisan serve'
      }
    }
    stage('run tests') {
      steps {
        sh 'php artisan test'
      }
    }
  }
}

def fileExists(filename) {
  return fileExists(new File(filename))
}

def fileExists(file) {
  return file.exists()
}