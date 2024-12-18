pipeline {
  agent any
  stages {
    stage('Checkout code') {
      steps {
        git(url: 'https://github.com/kacienewsom/cnewsom.github.io', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Front-end unit tests') {
          steps {
            sh 'npm i && npm run test:unit'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'docker build . '
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_USER = 'kacienewsom'
        DOCKERHUB_PASSWORD = 'LmBt1tCyBbAtT!'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}