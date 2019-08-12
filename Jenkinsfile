pipeline {
  agent any
  libraries {
    lib('')
  }
  stages {
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