
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "akshatha29/docimg"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/akshatha1990M/docker2026.git'
            }
        }

        stage('Build Docker Image') {
    steps {
        bat 'docker build -t %DOCKER_IMAGE%:latest .'
    }
}

        stage('Login to Docker Hub') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub-creds',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {
            bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
        }
    }
}

stage('Push Docker Image') {
    steps {
        bat 'docker push %DOCKER_IMAGE%:latest'
    }
}
    }

    post {
        success {
            echo 'Image successfully built and pushed to Docker Hub'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}

