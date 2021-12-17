pipeline {
  agent any
     
  
environment {
   build_result= 'SUCCESS'
}
  
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn clean'
        }
        //influxDbPublisher(selectedTarget: 'satdb')
         }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn test'
        }
        //influxDbPublisher(selectedTarget: 'satdb')
      }
    }

    stage('Deploy') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn package'
        }
        
        
        influxDbPublisher customPrefix: '', customProjectName: '', jenkinsEnvParameterField: '', jenkinsEnvParameterTag: '', selectedTarget: 'satdb'
      }
    }
   
  }
}
