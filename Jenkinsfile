pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn clean'
        }
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn test'
        }
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }

    stage('Deploy') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn package'
        }
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }
   
  }
}
