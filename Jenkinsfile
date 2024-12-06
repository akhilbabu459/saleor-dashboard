pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main', url: 'https://github.com/WorkshopsByKhaja/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                // Fix the typo in the Docker image name
                sh 'docker image build -t shaikkhajaibrahim/saleor-dashboard:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                // Use Jenkins credentials securely for Docker login
                withCredentials([usernamePassword(credentialsId: '12345', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // Login to Docker Hub using credentials
                    sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                    // Push the Docker image to Docker Hub
                    sh 'docker image push shaikkhajaibrahim/saleor-dashboard:DEV'
                }
            }
        }
    }
}
