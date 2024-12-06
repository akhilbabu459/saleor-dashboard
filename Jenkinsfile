pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "https://hub.docker.com/u/akhil1919:latest"
        DOCKER_REGISTRY = "https://hub.docker.com/u/akhil1919"
        DOCKER_CREDENTIALS = "123123" // Jenkins credentials ID for Docker login
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/akhilbabu459/saleor-dashboard.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Login to Docker Registry') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "$DOCKER_CREDENTIALS", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
    post {
        always {
            cleanWs() // Clean workspace after the job
        }
    }
}
