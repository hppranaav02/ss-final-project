 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       script {
         // Replace 'grype' with the full path to the grype executable if needed
         def grypeParam = params.GRYPE_OPTION
       
         def grypeCommand = '/usr/local/bin/grype ${grypeParama}'
       
         def grypeReportFile = 'grype_report.txt'

         // Run Grype and redirect the output to a file
         sh "${grypeCommand} > ${grypeReportFile}"

         // You can also archive the report as an artifact
         archiveArtifacts artifacts: "${grypeReportFile}", onlyIfSuccessful: true
       }
      }
    }
  }
}
