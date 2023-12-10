 pipeline {
  agent any
  environment {
        GRYPE_PATH = sh(script: 'which grype', returnStdout: true).trim()
   }
  stages {
     stage('Grype scan') {
      steps {
       sh ' ${GRYPE_PATH} postgres:9 --scope AllLayers --fail-on=critical'
      }
    }
  }

  post {
    always {
      node {
        // Record and manage issues
        recordIssues(
          tools: [grype()],
          aggregatingResults: true,
          failedNewAll: 1, // fail if >= 1 new issues
          failedTotalHigh: 20, // fail if >= 20 HIGHs
          failedTotalAll: 100, // fail if >= 100 issues in total
          filters: [
            excludeType('CVE-2023-2976'),
            excludeType('CVE-2012-17488'),
          ],
          // failOnError: true
        )
      }
    }
  }
}
