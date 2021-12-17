pipeline {
  agent any
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
         }
    }
  
  }
   post {
        always {
            influxDbPublisher customPrefix: '', customProjectName: '', jenkinsEnvParameterField: '''
            tribe=tribe_name
            squad=squad_name
            application_name=app_name
            product_name=product_name
''', jenkinsEnvParameterTag: '', selectedTarget: 'satdb' 
           }
     }
