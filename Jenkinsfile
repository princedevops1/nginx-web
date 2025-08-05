pipeline {
    agent any
    environment {
        IMAGE_NAME = 'princedevops08/nginx-web'
    }
    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/princedevops1/nginx-web.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
