pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pulls the code from GitHub
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // 'sh' runs commands in the terminal
                // This builds the image using the Dockerfile in your repo
                sh 'docker build -t my-web-app:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                // Stop the old container if it exists, then run the new one
                sh 'docker stop my-running-app || true'
                sh 'docker rm my-running-app || true'
                sh 'docker run -d -p 80:80 --name my-running-app my-web-app:latest'
            }
        }
    }
}
