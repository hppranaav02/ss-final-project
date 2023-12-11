 pipeline {
  agent any
  stages {
     stage('Grype scan') {
      steps {
       script {       
         def grypeReportFile = '/Users/pradeep/.jenkins/workspace/sss-test/grype-report.json'

         // Run Grype and redirect the output to a file
         sh "/usr/local/bin/grype ${params.GRYPE_OPTION} -o json > ${grypeReportFile}"

         // You can also archive the report as an artifact
         // archiveArtifacts artifacts: "${grypeReportFile}", onlyIfSuccessful: true
       }
      }
    }

  stage('Anchore Scan') {
   steps {
    script {
//             sh '''
//          curl -X 'POST' \
//   'http://localhost:8228/images?force=false&autosubscribe=false' \
//   -H 'accept: application/json' \
//   -H 'x-anchore-account: admin' \
//   -H 'Content-Type: application/json' \
//   -d '{
//   "dockerfile": "3JtqegE",
//   "digest": "string",
//   "tag": "string",
//   "created_at": "2023-12-10T22:35:02.935Z",
//   "image_type": "string",
//   "annotations": {},
//   "source": {
//     "import": {
//       "contents": {
//         "packages": "string",
//         "image_config": "string",
//         "manifest": "string",
//         "parent_manifest": "string",
//         "dockerfile": "string"
//       },
//       "tags": [
//         "docker.io/library/nginx:latest"
//       ],
//       "digest": "string",
//       "parent_digest": "string",
//       "local_image_id": "string",
//       "operation_uuid": "string"
//     }
//   }
// }'
//         '''
     
       sh " /Users/pradeep/Library/Python/3.9/bin/anchore-cli --u admin --p foobar image add ${params.GRYPE_OPTION}  "
     
       sh " /Users/pradeep/Library/Python/3.9/bin/anchore-cli --u admin --p foobar image wait ${params.GRYPE_OPTION}"
     
       sh " /Users/pradeep/Library/Python/3.9/bin/anchore-cli --u admin --p foobar image vuln ${params.GRYPE_OPTION}"
     
       sh " /Users/pradeep/Library/Python/3.9/bin/anchore-cli --u admin --p foobar evaluate check ${params.GRYPE_OPTION} --detail  > anchore_policy_check.txt"

       // Check if the string "Status: fail" exists in the text file
       def searchString = 'Status: fail'
       def textFilePath = 'anchore_policy_check.txt'

       if (fileContainsString(textFilePath, searchString)) {
           error "Build failed: Anchore Policy Check Failed"
       } else {
           echo "Stage passed. Anchore Policy Check passed"
       }
     
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

def fileContainsString(filePath, searchString) {
    def fileContents = readFile(filePath).trim()
    return fileContents.contains(searchString)
}
