 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       script {
         // Replace 'grype' with the full path to the grype executable if needed
       
         // def grypeReportFile = '/Users/pradeep/.jenkins/workspace/sss-test/grype-report.json'

         // // Run Grype and redirect the output to a file
         // sh "/usr/local/bin/grype ${params.GRYPE_OPTION} -o json > ${grypeReportFile}"

         // // You can also archive the report as an artifact
         // archiveArtifacts artifacts: "${grypeReportFile}", onlyIfSuccessful: true

        sh '''
         curl -X 'POST' \
  'http://localhost:8228/images?force=false&autosubscribe=false' \
  -H 'accept: application/json' \
  -H 'x-anchore-account: admin' \
  -H 'Content-Type: application/json' \
  -d '{
  "dockerfile": "3JtqegE",
  "digest": "string",
  "tag": "string",
  "created_at": "2023-12-10T22:35:02.935Z",
  "image_type": "string",
  "annotations": {},
  "source": {
    "import": {
      "contents": {
        "packages": "string",
        "image_config": "string",
        "manifest": "string",
        "parent_manifest": "string",
        "dockerfile": "string"
      },
      "tags": [
        "docker.io/library/nginx:latest"
      ],
      "digest": "string",
      "parent_digest": "string",
      "local_image_id": "string",
      "operation_uuid": "string"
    }
  }
}'
        '''
       }
      }
    }
  }
  post {
    always {
     recordIssues enabledForFailure: true, tool: grype()
    }
  }
}
