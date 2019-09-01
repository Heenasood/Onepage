pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      environment {
        param1 = 'One Default'
        param2 = 'Parameter2'
      }
      parallel {
        stage('SharedLibraryStep') {
          steps {
            node(label: 'master') {
              script {
                @Library('myFirstLibrary')_

                stage('Print Build Info') {
                  printBuildinfo {
                    name = "Heena Sood"
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
        stage('PrintMsg') {
          steps {
            node(label: 'NewSlave') {
              echo 'Print message on Slave Node'
            }

          }
        }
      }
    }
    stage('Print Success') {
      steps {
        echo 'Both the nodes has been executed'
      }
    }
  }
  environment {
    BuildName = 'EnteringIntoSharedPipe'
  }
}