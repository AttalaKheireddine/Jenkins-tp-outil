pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc '
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build/test-results/test/*'
      }
    }

    stage('Mail notification') {
      steps {
        mail(subject: 'Dela3', body: 'Dela3', to: 'gk_attala@esi.dz')
      }
    }

  }
}