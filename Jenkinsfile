pipeline {
  agent any
  stages {
    stage('SharedLibraryStep') {
      environment {
        param1 = 'One Default'
        param2 = 'Parameter2'
        dev = 'dev'
        qa = 'qa'
      }
      parallel {
        stage('Interactive_Input') {
          steps {
            script {
              def inputConfig
              def inputTest

              // Get the input
              def userInput = input(
                id: 'userInput', message: 'Enter path of test reports:?',
                parameters: [

                  string(defaultValue: 'None',
                  description: 'Path of config file',
                  name: 'Config'),
                  string(defaultValue: 'None',
                  description: 'Test Info file',
                  name: 'Test'),
                ])

                // Save to variables. Default to empty string if not found.
                inputConfig = userInput.Config?:'heena1'
                inputTest = userInput.Test?:'heena2'

                // Echo to console
                echo("IQA Sheet Path: ${inputConfig}")
                echo("Test Info file path: ${inputTest}")

                // Write to file
                writeFile file: "inputData.txt", text: "Config=${inputConfig}\r\nTest=${inputTest}"

                // Archive the file (or whatever you want to do with it)
                archiveArtifacts 'inputData.txt'
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
      stage('Use Deployment Parameters') {
        steps {
          script {
            echo "All parameters have been set as Environment Variables"
            echo "Selected Environment: ${params.select_environment}"
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
      qa = 'qa'
      dev = 'dev'
    }
    parameters {
      choice(name: 'select_environment', choices: '''dev
qa
prod''', description: 'Select environment')
    }
  }