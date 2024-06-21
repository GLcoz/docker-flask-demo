pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('my_docker_credentials')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                script {
                    sh 'docker build -t hakimedy/flaskapp:$BUILD_NUMBER .'
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    sh 'docker push hakimedy/flaskapp:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            script {
                node {
                    sh 'docker logout'
                }
            }
        }
    }
}
