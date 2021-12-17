pipeline {
  agent any
  stages {
    stage('ls -l') {
      steps {
            sh 'ls -l'
          }
    }

    stage('ld') {
      steps {
        sh 'ld'
      }
    }
  }
   post {
        always {
            influxDbPublisher customPrefix: '', customProjectName: '', jenkinsEnvParameterField: '''f1=ali
            f2=arezo
            f3=david

''', jenkinsEnvParameterTag: '', selectedTarget: 'satdb' 
           }
     }
}
