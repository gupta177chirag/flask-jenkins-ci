pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yourdockerhub/flask-jenkins-project'
    }

    stages {
       stage('Clone') {
    steps {
        git branch: 'main', url: 'https://github.com/gupta177chirag/flask-jenkins-ci.git'
    }
}

        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE_NAME
                    '''
                }
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker stop flask-jenkins-project || true
                docker rm flask-jenkins-project || true
                docker run -d -p 5000:5000 --name flask-jenkins-project $IMAGE_NAME
                '''
            }
        }
    }
}