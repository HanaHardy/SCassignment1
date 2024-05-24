pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("yourusername/your-repo:latest")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Add your test steps here
                    sh 'echo "Running tests..."'
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS_ID}") {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
