pipeline {
    agent any
    tools {
        go 'go-1.17'
    }
    environment{
        GO111MODULE='on'

    }
    stages {
        stage('Build or Compile') {
            steps {
               sh 'go build .'
            }
        }

        stage('Test') {
            steps {
                sh 'go test ./...'
            }
        }
		
		 stage('Release') {
            when {
                buildingTag()
            }
            environment {
                GITHUB_TOKEN = credentials('github_token')
            }
            steps {
                sh 'curl -sL https://git.io/goreleaser | bash'
            }
        }
        
    }
}
