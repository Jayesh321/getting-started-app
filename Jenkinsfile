pipeline {
    agent any

    environment {
        IMAGE_NAME = "getting-started-app"
        TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t ${IMAGE_NAME}:${TAG} .
                """
            }
        }

        stage('Run container') {
            steps {
                sh """
                    docker run -d --name test-app -p 3000:3000 ${IMAGE_NAME}:${TAG}
                """
            }
        }

        stage('Verify') {
            steps {
                sh "docker ps"
            }
        }
    }

    post {
        always {
            sh "docker stop test-app || true"
            sh "docker rm test-app || true"
        }
    }
}
