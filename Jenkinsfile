pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/vikasvajroju23531933/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t vajroju/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push vajroju/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

