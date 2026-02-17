pipeline {
    agent any
    stages {
        stage('Pull Code') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                // This builds the image inside the Jenkins workspace
                sh 'docker build -t webhookautomation:latest .'
            }
        }
        stage('Deploy') {
            steps {
                // Stop any old container with the same name to avoid conflicts
                sh 'docker stop my-live-app || true'
                sh 'docker rm my-live-app || true'
                // Run the new container
                sh 'docker run -d -p 80:80 --name my-live-app webhookautomation:latest'
            }
        }
    }
}
