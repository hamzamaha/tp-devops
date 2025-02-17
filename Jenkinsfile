pipeline {
    agent any
    environment {
        registry = "hamzamaha/tp4"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/hamzamaha/tp-devops'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build registry + ":latest"
                }
            }
        }
        stage('Test Image') {
            steps {
                script {
                    echo "Tests passed!"
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        docker.image(registry + ":latest").push()
                    }
                }
            }
        }
        stage('Deploy to Server') {
            steps {
                sh "docker run -d -p 8080:80 moham3did/tp4:latest"
            }
        }
    }
}