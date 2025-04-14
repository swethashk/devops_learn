pipeline {
    agent any

    environment {
        IMAGE_NAME = 'hello-jenkins-docker'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo '🛠️ Building Docker image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo '🐳 Running Docker container...'
                sh 'docker run --rm $IMAGE_NAME'
            }
        }
    }
}
