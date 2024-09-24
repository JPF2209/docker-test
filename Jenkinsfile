pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('6_2hd')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git branch:'main', url:'https://github.com/JPF2209/docker-test.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t jpf2209/6_2hd:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push jpf2209/6_2hd:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
