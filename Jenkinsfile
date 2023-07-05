pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-ashok1043')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Bhargav-LNSN/docker-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ashok1043/docker_practice:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ashok1043/docker_practice:$BUILD_NUMBER'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull ashok1043/docker_practice:$BUILD_NUMBER'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 443:80 ashok1043/docker_practice:$BUILD_NUMBER'
            }
        }   
        
}
post {
        always {
            sh 'docker logout'
        }
    }
}

