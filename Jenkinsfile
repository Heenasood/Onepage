pipeline {
  agent any
  stages {
    stage('library') {
      steps {
        library 'myFirstLibrary'
      }
    }
    stage('Deploy2') {
      steps {
        libraryResource 'deploy'
      }
    }
    stage('Deploy') {
      steps {
        load 'deploy()'
      }
    }
    stage('Enable balancer') {
      steps {
        load 'enableBalancerUtils()'
      }
    }
    stage('Check Status') {
      steps {
        load 'checkStatus()'
      }
    }
  }
  environment {
    BuildName = 'EnteringIntoSharedPipe'
  }
}