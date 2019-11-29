pipeline {
  agent any
  stages {
    stage('updating secrets on Hassio'){
      steps {
        sh'scp /homeassistant/secrets.yaml root@hassio.local:/config/secrets.yaml'
      }
    }
  }
}