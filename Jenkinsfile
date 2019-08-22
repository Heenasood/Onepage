pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      steps {
        node(label: 'master') {
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

        }

      }
    }
    stage('Print Success') {
      steps {
        node(label: 'NewSlave') {
          echo 'Shared Library step has been successfully executed'
        }

      }
    }
  }
  environment {
    BuildName = 'EnteringIntoSharedPipe'
  }
}