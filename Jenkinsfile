pipeline {
  agent any
  stages {
    stage('libra') {
      steps {
        library 'myFirstLibrary'
      }
    }
    stage('Disable balancer') {
      steps {
        libraryResource 'disableBalancerUtils'
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
    BuildName = 'EnteringInteoSharedPipe'
  }
}