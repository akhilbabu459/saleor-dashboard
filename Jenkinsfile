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
                // Correct the image tag here, ensure it's correctly named
                sh 'docker image build -t shaikkhajaibrahim/saleor-dashboard:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                // Use Jenkins Credentials to securely handle Docker login
                withCredentials([usernamePassword(credentialsId: 'docker-credentials-id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                    // Push the image to Docker Hub
                    sh 'docker image push shaikkhajaibrahim/saleor-dashboard:DEV'
                }
            }
        }
    }
}
