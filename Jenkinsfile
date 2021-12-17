pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn clean'
        }
        try {
            // Build things here
        if (currentBuild.result == null) {
            currentBuild.result = 'SUCCESS' // sets the ordinal as 0 and boolean to true
         }
        } catch (err) {
           if (currentBuild.result == null) {
            currentBuild.result = 'FAILURE' // sets the ordinal as 4 and boolean to false
          }
        throw err
        } finally {
           influxDbPublisher(selectedTarget: 'david_influxdb')
        }
        
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
