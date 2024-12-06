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
        
    }
}
