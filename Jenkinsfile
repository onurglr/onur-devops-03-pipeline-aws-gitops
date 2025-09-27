pipeline {
    agent any
    environment {
        APP_NAME = "devops-03-pipeline-aws-onur"
    }

         stages {
              stage('Cleanup Workspace') {
            steps {
                script {
                  cleanWs()
                }
            }
        }
        stage('SGM Github') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/onurglr/onur-devops-03-pipeline-aws-gitops']])
            }
        }
             stage("Update the Deployment Tags") {
    steps {
        powershell '''
           Write-Host "Before update:"
           Get-Content deployment.yaml

           (Get-Content deployment.yaml) `
             -replace "image: *onurguler18/devops-03-pipeline-aws-onur:.*", "image: onurguler18/devops-03-pipeline-aws-onur:${env:IMAGE_TAG}" `
             | Set-Content deployment.yaml

           Write-Host "After update:"
           Get-Content deployment.yaml
        '''
    }
}
stage("Push the changed deployment file to Git") {
  steps {
    withCredentials([usernamePassword(
      credentialsId: 'github_token',
      usernameVariable: 'GIT_USER',
      passwordVariable: 'GIT_TOKEN'
    )]) {
      powershell '''
        $ErrorActionPreference = "Stop"

        git config user.name "onurglr"
        git config user.email "onurguler18@gmail.com"

        try {
            git checkout -B main origin/main
        } catch {
            Write-Host "Branch checkout skipped or not needed."
        }

        git add deployment.yaml

        git diff --cached --quiet
        if ($LASTEXITCODE -eq 0) {
            Write-Host "No changes to commit."
            exit 0
        }

        git commit -m "Updated Deployment Manifest"

        $repoUrl = "https://${env:GIT_USER}:$($env:GIT_TOKEN)@github.com/onurglr/onur-devops-03-pipeline-aws-gitops"
        git push $repoUrl HEAD:main
      '''
    }
  }
}


             
        
    }
}
