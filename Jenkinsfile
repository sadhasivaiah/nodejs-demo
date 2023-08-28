pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-hareeshpdocker')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/hareeshpgit/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t sadasivaiah01/nginx-docker-image:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push sadasivaiah01/nginx-docker-image:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull sadasivaiah01/nginx-docker-image:$BUILD_NUMBER'
            }
        }
        stage('run image') {
            steps{
                sh 'docker run -d -p 80:80 sadasivaiah01/nginx-docker-image:$BUILD_NUMBER'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

