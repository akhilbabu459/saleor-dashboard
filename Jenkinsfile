

pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    environment {
        DOCKER_USERNAME = 'akhilp95'
        DOCKER_PASSWORD = 'Ramadevip@11'
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main', url: 'https://github.com/WorkshopsByKhaja/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                sh 'docker image build -t shaikkhajaibrahim/saleor-dashboar:DEV .'
            }
        }
        stage('push image to registry') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                sh 'docker image push shaikkhajaibrahim/saleor-dashboar:DEV'
            }
        }
    }
}

