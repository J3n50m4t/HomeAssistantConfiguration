node {
    stage('updating git') { 
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/J3n50m4t/HomeAssistantConfiguration.git']]])
    }
   stage('Preparation') { // for display purposes
      sh'ssh root@hassio.local "cd /config/ && pwd && git pull"'
   }
    stage('updating secrets on Hassio'){
       sh'scp /homeassistant/secrets.yaml root@hassio.local:/config/secrets.yaml'
   }
} 