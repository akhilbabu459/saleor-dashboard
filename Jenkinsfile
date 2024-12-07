pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            agent { label 'build' }
            steps {
                git branch: 'dev', url: 'https://github.com/akhilbabu459/storefront.git'
            }
        }
        stage('docker image build') {
            agent { label 'build' }
            steps {
                sh 'docker image build -t akhil1919/saleor-front:DEV .'
            }
        }
        stage('push image to registry') {
            agent { label 'build' }
            steps {
                sh 'docker image push akhil1919/saleor-front:DEV'
            }
        }
        stage('create terraform infrastructre') {
            agent { label 'terraform' }
            steps {
                git url: 'git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster'
                sh 'terraform init && terraform apply -auto-approve'
            }
        }
    }
}
