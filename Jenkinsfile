pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
        GITHUB_CREDENTIALS_ID = 'github-token'
        IMAGE_NAME = 'hanahardy/scassignment'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the code from the GitHub repository
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/HanaHardy/SCassignment.git',
                            credentialsId: "${GITHUB_CREDENTIALS_ID}"
                        ]]
                    ])
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    // Build the Docker image with the specified tag
                    dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
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
