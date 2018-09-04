def GitUrl= 'https://github.com/466300750/api-workshop-105'
def GitBranch= '*/master'

pipeline {
  agent any
  stages {
    stage('checkout_source') {
            steps {
                sh """
                if [[ -d $WORKSPACE ]];then
                    rm -rf $WORKSPACE/*
                fi
                """
                checkout([$class: 'GitSCM', branches: [[name: "${GitBranch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: "${GitUrl}"]]])
            }
        }

      stage('publish_image') {
          steps {
              sh """
                order-service/publish_image
                """
          }
      }

      stage('deploy') {
            steps {
                sh """
                order-service/deploy
                """
            }
      }
  }
}