pipeline {
  agent any
  stages {
    stage('libra') {
      steps {
        library 'myFirstLibrary'
      }
    }
    stage('Print Build Info') {
      steps {
        echo 'Print Build Info: ${BuildName}'
      }
    }
    stage('Disable balancer') {
      steps {
        load 'disableBalancerUtils()'
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