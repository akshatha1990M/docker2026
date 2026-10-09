
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

       stage('Login to Docker Hub') {
steps {
withCredentials([usernamePassword(
credentialsId: 'dockerhub-creds',
usernameVariable: 'DOCKER_USER',
passwordVariable: 'DOCKER_PASS'
)]) {
powershell '''
if ([string]::IsNullOrWhiteSpace($env:DOCKER_PASS)) {
Write-Error "Docker Hub token is empty"
exit 1
}

            Write-Host "Docker Hub username: $env:DOCKER_USER"
            Write-Host "Token is present"

            $env:DOCKER_PASS | docker login -u $env:DOCKER_USER --password-stdin

            if ($LASTEXITCODE -ne 0) {
                exit 1
            }
        
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

