pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('ad7cd53f-3449-4b14-8844-e817562d0f06	')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/JPF2209/docker-test.git'
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

