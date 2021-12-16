pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean'
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }

    stage('Deploy') {
      steps {
        sh 'mvn package'
        influxDbPublisher(selectedTarget: 'david_influxdb')
      }
    }
   
  }
}
