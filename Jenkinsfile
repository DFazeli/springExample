pipeline {
  agent any
  def myFields = [:]
      myFields['tribe'] = CoreIT
      myFields['squad'] = SQUAD
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn clean'
        }
        
      }
    }

    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn test'
        }
        
      }
    }

    stage('Deploy') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
           sh 'mvn package'
        }
        
      }
    }
   influxDbPublisher(selectedTarget: 'david_influxdb', customData: myFields)
  }
}
