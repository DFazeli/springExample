pipeline {
  agent any
  
  environment {
    buildResult= 'SUCCESS'
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
        //influxDbPublisher(selectedTarget: 'satdb')
        influxDbPublisher customPrefix: '', customProjectName: '', jenkinsEnvParameterField: '''f1=core f2=zeus f3=zeuss''', jenkinsEnvParameterTag: '', selectedTarget: 'satdb'
      }
    }
   
  }
}
