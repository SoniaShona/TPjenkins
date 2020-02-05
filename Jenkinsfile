pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/**.jar'
        archiveArtifacts(artifacts: 'build/reports/**', allowEmptyArchive: true)
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'build', body: 'succes du build', to: 'gs_reffad@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test Report') {
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

    stage('Slack Notification') {
      steps {
        slackSend(token: 'TTJA9NG6Q/BTK232E9E/AK7PCjP9dzFsVilLNFUoq9VJ', baseUrl: 'https://hooks.slack.com/services/', teamDomain: 'tp8outils', channel: '#jenkins', sendAsText: true, message: 'Déployé avec succès')
      }
    }

  }
}
