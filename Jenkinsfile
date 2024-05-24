pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git url: 'https://github.com/hanahardy/SCassignment.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    dockerImage = docker.build("hanahardy/scassignment:latest")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Add your test steps here
                    sh 'echo "Running tests..."'
                    // Example test command:
                    // sh 'docker run --rm hanahardy/scassignment:latest some-test-command'
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS_ID}") {
                        // Push the Docker image to Docker Hub
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
