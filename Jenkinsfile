pipeline {
    agent any
      environment {
        NAME = 'Gimmy'
        LASTNAME = 'Muller'
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
        
        stage('Final')
        {
            steps
            {
                sh 'echo this is the final stage'
                
                
            }
            
            
            
        }
        
        
    }
}
