pipeline {
    agent none

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
    }

    stages {
        stage('Build') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:3.1' }
            }
            steps {
                sh 'pwd'
                sh 'ls'
                sh 'cd DotnetTemplate.Web'
                sh 'ls'
                sh 'dotnet build'
            }
        }
        stage('dotnet Test') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:3.1' }
            }
            steps {
                sh 'cd DotnetTemplate.Web.Tests'
                sh 'dotnet test'
            }
        }
        stage('npm Test') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm i && npm t && npm run lint'
            }
        }
    }
}
