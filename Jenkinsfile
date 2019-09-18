pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
		stage('Veracode DevOps Scan') {
      steps {
        - sh 'curl -O https://downloads.veracode.com/securityscan/devops-scanner-java-LATEST.zip'
        - sh 'unzip devops-scanner-java-LATEST.zip devops-scanner-java.jar'
        - sh 'java -jar devops-scanner-java.jar \
          --api_id "${VERACODE_API_ID}" \
          --api_secret_key "${VERACODE_API_SECRET}" \
          --project_name "verademo" \
          --j target/veradeom.war'
		}
        // stage('Greenlight Example') {
		//     steps {
		// 		withCredentials([usernamePassword(credentialsId: '902d2462-e536-4927-9398-d2ab0dae85a1', passwordVariable: 'vkey', usernameVariable: 'vid')]) {

		// 			powershell '''
		// 				$dir = (Get-Item -Path ".\\").FullName
		// 				$zipupload = $dir + \'gl-scanner-java-LATEST.zip\';
		// 				(New-Object Net.WebClient).DownloadFile(\'https://downloads.veracode.com/securityscan/gl-scanner-java-LATEST.zip\',$zipupload);

		// 				function Unzip($zipfile, $outdir)
		// 				{
		// 					Add-Type -AssemblyName System.IO.Compression.FileSystem
		// 					$archive = [System.IO.Compression.ZipFile]::OpenRead($zipfile)
		// 					foreach ($entry in $archive.Entries)
		// 					{
		// 						$entryTargetFilePath = [System.IO.Path]::Combine($outdir, $entry.FullName)
		// 						$entryDir = [System.IO.Path]::GetDirectoryName($entryTargetFilePath)

		// 						#Ensure the directory of the archive entry exists
		// 						if(!(Test-Path $entryDir )){
		// 							New-Item -ItemType Directory -Path $entryDir | Out-Null 
		// 						}

		// 						#If the entry is not a directory entry, then extract entry
		// 						if(!$entryTargetFilePath.EndsWith("\\")){
		// 							[System.IO.Compression.ZipFileExtensions]::ExtractToFile($entry, $entryTargetFilePath, $true);
		// 						}
		// 					}
		// 				}

		// 				Unzip -zipfile "$zipupload" -outdir "$dir"
		// 			'''

		// 			bat """\
		// 				java -jar ./gl-scanner-java.jar \
		// 					--api_id "${vid}" \
		// 					--api_secret_key "${vkey}" \
		// 					--project_name "${env.JOB_NAME}" \
		// 					--project_url "${env.JOB_URL}" \
		// 					--project_ref "${env.GIT_COMMIT}" \
		// 				"""
		// 					// --issue_details true \
		// 					// --issue_counts=5:0,4:0,3:0,2:0,1:0,0:0 \
        //         }
		//     }
		// }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
	// post {
	//     always {
	//       archiveArtifacts artifacts: 'results.json', fingerprint: true
	//     }
	// }
}
