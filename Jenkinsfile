 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       script {
         // Replace 'grype' with the full path to the grype executable if needed
       
         def grypeReportFile = 'grype_report.txt'

         // Run Grype and redirect the output to a file
         sh "/usr/local/bin/grype ${params.GRYPE_OPTION} > ${grypeReportFile}"

         // You can also archive the report as an artifact
         archiveArtifacts artifacts: "${grypeReportFile}", onlyIfSuccessful: true
       }
      }
    }
  }
}
