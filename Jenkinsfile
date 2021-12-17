pipeline {
  agent any
  environment {
    currentBuild.result = 'SUCCESS'
  }
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn clean'
        }
        influxDbPublisher(selectedTarget: 'satdb')
         }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn test'
        }
        influxDbPublisher(selectedTarget: 'satdb')
      }
    }

    stage('Deploy') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn package'
        }
        influxDbPublisher(selectedTarget: 'satdb')
      }
    }
   
  }
}
