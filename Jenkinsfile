pipeline {
  agent any
  stages {
    stage('Build') {
      when {
        expression {
          env.CHANGE_ID == null
        }
      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc '
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build/test-results/test/*'
      }
    }

    stage('Mail notification') {
      when {
        expression {
          env.CHANGE_ID == null
        }
      }
      steps {
        mail(subject: 'mail notification', body: 'mail notif', to: 'gk_attala@esi.dz')
      }
    }

    stage('Code Analysis') {
      when {
        expression {
          env.CHANGE_ID == null
        }
      }
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test reporting') {
          steps {
            jacoco()
          }
        }

      }
    }

    stage('Deployment') {
      
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack notification') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', token: 'TRQC12GGL/BT7843G5C/OROqdzn83cUuhBvoBTLlchHc', channel: 'tp', teamDomain: 'tp-outil', message: 'Salam ailkom')
      }
    }

  }
}
