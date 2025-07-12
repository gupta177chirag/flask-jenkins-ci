pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/gupta177chirag/flask-jenkins-ci.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    sh 'docker build -t flask-jenkins-app .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    sh 'docker tag flask-jenkins-app chirag177gupta/flask-jenkins-app:latest'
                    sh 'docker push chirag177gupta/flask-jenkins-app:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the Docker container..."
                    sh 'docker stop flask-jenkins-container || true'
                    sh 'docker rm flask-jenkins-container || true'
                    sh 'docker run -d -p 5001:5000 --name flask-jenkins-container chirag177gupta/flask-jenkins-app:latest'
                }
            }
        }
    }
}
