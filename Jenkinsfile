pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-app"   // Change this to your app name
        IMAGE_TAG = "latest"
        DOCKER_HUB_REPO = "saikotgirep/saikotgirep" // Change this accordingly
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SaiKotgire/TeatRepo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t myapp:latest ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    script {
                        sh "docker tag myapp:latest saikotgirep:latest"
                        sh "docker push saikotgirep:latest"
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh "docker rmi myapp:latest || true"
                    sh "docker rmi saikotgirep:latest || true"
                }
            }
        }
    }
}
