pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // This triggers the pipeline to run every minute; you can adjust the cron schedule as needed
    }
    stages {
        stage('vcs') {
            steps {
                // Update the Git repository URL to the new one
                git branch: 'main', url: 'https://github.com/akhilbabu459/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                // Build Docker image with the correct tag
                sh 'docker image build -t akhil/saleor-dashboar:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                // Push Docker image to the registry
                sh 'docker image push akhil/saleor-dashboar:DEV'
            }
        }
    }
}
