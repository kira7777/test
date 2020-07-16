pipeline {
  agent any
  stages {
    stage('Test_dev') {
      parallel {
        stage('Test_dev') {
          steps {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              timeout(time: 6, unit: 'SECONDS') {
                retry(count: 3) {
                  sh 'echo hello, this is was edited bu Blu Ocean Editor'
                  sh 'sleep 3'
                }

              }

              sh 'echo 2nd step of the Test stage: execute by $NAME , $LASTNAME'
            }

          }
        }

        stage('') {
          steps {
            sh 'echo this stage created on Blue Ocean'
          }
        }

      }
    }

    stage('CodeFixAndValidation_dev') {
      parallel {
        stage('CodeFix_dev') {
          steps {
            sh 'echo "success! ha Blue Ocean"; exit 0'
          }
        }

        stage('CodeValidation_dev') {
          steps {
            sh 'echo "the Code Validation Stage"; exit 0'
          }
        }

      }
    }

    stage('Final_dev') {
      steps {
        sh """
                                   echo 'this is the final stage'
                                   echo 'by the way this is the secret of $NAME : $secret ' 
                                     
                                   """
      }
    }

  }
  environment {
    NAME = 'Gimmy_the_Dev'
    LASTNAME = 'Muller_Blue'
    secret = credentials('My_SECRET')
  }
  post {
    always {
      echo 'I will always get executed :D'
    }

    success {
      echo 'I will only get executed if this success'
    }

    failure {
      echo 'I will only get executed if this fails'
    }

    unstable {
      echo 'I will only get executed if this is unstable'
    }

  }
}