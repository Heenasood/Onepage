pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      environment {
        param1 = 'One Default'
        param2 = 'Parameter2'
        Environment = 'dev'
      }
      parallel {
        stage('Gather Deployment Parameters') {
          steps {
            timeout(time: 30, unit: 'SECONDS') {
              script {
                def INPUT_PARAMS = input message: 'Please Provide Parameters', ok: 'Next',
                parameters: [
                  choice(name: 'ENVIRONMENT', choices: ['dev','qa'].join('\n'), description: 'Please select the Environment')]
                  env.ENVIRONMENT = INPUT_PARAMS.ENVIRONMENT
                }

              }

            }
          }
          stage('Use Deployment Parameters') {
            steps {
              script {
                echo "All parameters have been set as Environment Variables"
                echo "Selected Environment: ${env.ENVIRONMENT}"
              }

            }
          }
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