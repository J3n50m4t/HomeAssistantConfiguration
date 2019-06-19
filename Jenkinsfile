pipeline {
  agent any
  environment { 
    HOMEASSISTANT_AUTH_KEY = credentials('jenkins-homeassistant-auth-key')
    HOMEASSISTANT_URL = credentials('jenkins-homeassistant-domain')
  }
  stages {
    stage('updating Git') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/J3n50m4t/HomeAssistantConfiguration.git']]])
      }
    }
    stage('updating Git on Hassio') {
      steps {
        sh'ssh root@hassio.local "cd /config/ && pwd && git pull"'
      }
    }
    stage('updating secrets on Hassio'){
      steps {
        sh'scp /homeassistant/secrets.yaml root@hassio.local:/config/secrets.yaml'
      }
    }
    stage('check HA config') {
      steps {
        sh'curl -X POST -H \"Authorization: Bearer $HOMEASSISTANT_AUTH_KEY\" -H \"Content-Type: application/json\" https://$HOMEASSISTANT_URL/api/services/homeassistant/check_config'
      }
    }
    stage('restart HA ') {
      steps {
        sh'curl -X POST -H \"Authorization: Bearer $HOMEASSISTANT_AUTH_KEY\" -H \"Content-Type: application/json\" https://$HOMEASSISTANT_URL/api/services/homeassistant/restart'
      }
    }
  }
}