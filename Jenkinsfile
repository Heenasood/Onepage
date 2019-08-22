pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      steps {
        script {
          @Library('myFirstLibrary')_

          stage('Print Build Info') {
            printBuildinfo {
              name = "Sample Name"
            }
          } stage('Disable balancer') {
            disableBalancerUtils()
          } stage('Deploy') {
            deploy()
          } stage('Enable balancer') {
            enableBalancerUtils()
          } stage('Check Status') {
            checkStatus()
          }
        }

        node(label: 'master')
      }
    }
    stage('Print Success') {
      steps {
        echo 'Shared Library step has been successfully executed'
        node(label: 'NewSlave')
      }
    }
  }
  environment {
    BuildName = 'EnteringIntoSharedPipe'
  }
}