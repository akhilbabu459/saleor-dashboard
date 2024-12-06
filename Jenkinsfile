pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'main', url: 'https://github.com/akhilbabu459/saleor-dashboard.git'
            }
        }
        stage('docker image build') {
            steps {
                sh 'docker image build -t akhil1919/saleor-dashboard:latest .'
            }
        }
        stage('docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: "1233210", usernameVariable: 'akhil1919', passwordVariable: 'Ramadevip@11')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
            }
        }
        stage('push image to registry') {
            steps {
                sh 'docker image push akhil1919/saleor-dashboard:latest'
            }
        }
    }
}
