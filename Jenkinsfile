pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh """
                    docker build -t getting-started .
                """
            }
        }

        stage('Run Container') {
            steps {
                sh """
                    docker stop getting-started || true
                    docker rm getting-started || true
                    docker run -d --name getting-started -p 127.0.0.1:3000:3000 getting-started
                """
            }
        }
    }
}
