pipeline {
  agent any
  stages {
    stage('Test') {
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

    stage('CodeFixAndValidation') {
      parallel {
        stage('CodeFix') {
          steps {
            sh 'echo "success !"; exit 0'
          }
        }

        stage('CodeValidation') {
          steps {
            sh 'echo "the Code Validation Stage"; exit 0'
          }
        }

      }
    }

    stage('Final') {
      steps {
        sh """
                           echo 'this is the final stage'
                           echo 'by the way this is the secret of $NAME : $secret ' 
                             
                           """
      }
    }

  }
  environment {
    NAME = 'Gimmy'
    LASTNAME = 'Muller'
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