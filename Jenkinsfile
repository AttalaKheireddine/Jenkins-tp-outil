pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc '
        bat 'archiveArtifacts archives: \'build/docs/javadoc/*\''
      }
    }

  }
}