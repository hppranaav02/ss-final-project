 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       // Add Gruype installation path to PATH
       env.PATH = "${env.PATH}:/usr/local/bin/grype
       
       sh ' grype postgres:9 --scope AllLayers --fail-on=critical'
      }
    }
  }

post {
    always {
        recordIssues(
          tools: [grype()],
          aggregatingResults: true,
          failedNewAll: 1, //fail if >=1 new issues
          failedTotalHigh: 20, //fail if >=20 HIGHs
          failedTotalAll : 100, //fail if >=100 issues in total
          filters: [
            excludeType('CVE-2023-2976'),
            excludeType('CVE-2012-17488'),
          ],
          //failOnError: true
        )
    }
  }
}
