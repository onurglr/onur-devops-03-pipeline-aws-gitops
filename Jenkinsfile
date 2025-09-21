pipeline {
    agent {
        label 'My-Jenkins-Agent'
    }

    environment {
        APP_NAME = "onur-devops-03-pipeline-aws-gitops"
    }

         stages {
              stage('Cleanup Workspace') {
            steps {
                script {
                  CleanWs()
                }
            }
        }
        stage('SGM Github') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/onurglr/onur-devops-03-pipeline-aws-gitops']])
            }
        }


        
    }
}