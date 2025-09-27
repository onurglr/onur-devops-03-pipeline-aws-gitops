pipeline {
    agent any
    environment {
        APP_NAME = "onur-devops-03-pipeline-aws-gitops"
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


        
    }
}
