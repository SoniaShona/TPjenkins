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
        emailext(subject: 'Build Result TP8', body: 'build done', from: 'jenkins-notification@jenkins.com', to: 'gs_reffad@esi.dz')
      }
    }

  }
}