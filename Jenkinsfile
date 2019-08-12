pipeline {
  agent any
  stages {
    stage('Deploy2') {
      steps {
        library 'myFirstLibrary.deploy()'
      }
    }
    stage('Deploy') {
      steps {
        libraryResource 'myFirstLibrary.deploy()'
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