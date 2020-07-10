pipeline {
    agent any
      environment {
        NAME = 'Gimmy'
        LASTNAME = 'Muller'
        secret = credentials('My_SECRET')
    }
    stages {
        stage('Test') {
            steps {
                
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                timeout(time: 6, unit: 'SECONDS') {
                   retry(3) {
                    sh 'echo hello'
                     sh 'sleep 3'
                }
                }
                sh 'echo 2nd step of the Test stage: execute by $NAME , $LASTNAME'
                
                }
            }
            
        }
stage('Deploy') {
            steps {
                sh 'echo "Fail!"; exit 1'
            }
    }
        stage('Final')
        {
            steps
            {
                sh """
                   echo 'this is the final stage'
                   echo 'by the way this is the secret of $NAME : $secret ' 
                     
                   """ 
                
                
            }
            
            
            
        }

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
