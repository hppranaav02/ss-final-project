 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       sh ' /usr/local/bin/grype postgres:9 --scope AllLayers'
      }
    }
  }
}
