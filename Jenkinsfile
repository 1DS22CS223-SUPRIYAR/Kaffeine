pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sufiyasarwath/github-website@sha256:949d248af06df67c1f8426a62cd2ab344cc2b6fdf21ebb7587d7526f27ae2e2b'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/1DS22CS223-SUPRIYAR/Kaffeine.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE'
                    sh 'docker logout'
                }
            }
        }
    }
}
