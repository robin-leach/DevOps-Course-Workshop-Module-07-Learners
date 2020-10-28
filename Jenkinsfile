pipeline {
    agent none
  
    environment {
      DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
    }

    stages {  
        stage('Backend build') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk:3.1' }
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('Backend test') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk:3.1' }
            }
            steps {
                sh 'dotnet test'
            }
        }
        stage('Frontend build') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm install && npm run build'
            }
        }
        stage('Frontend test') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm run lint && npm t'
            }
        }
    }
}