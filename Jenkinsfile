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
        mail(subject: 'Build Result TP8', body: 'build done', to: 'gs_reffad@esi.dz', from: 'jenkins-notification@jenkins.com')
      }
    }

  }
}