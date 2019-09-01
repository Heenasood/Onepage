pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      parallel {
        stage('SharedLibraryStep') {
          steps {
            node(label: 'master') {
              script {
                @Library('myFirstLibrary')_

                stage('Print Build Info') {
                  printBuildinfo {
                    name = "Heena Sood"
                    env.param1 = "One default"
                    env.param2 = "TWO PARAMETER"
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