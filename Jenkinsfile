pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('my_docker_credentials')
    }
    stages {
        stage('Build docker image') {
            steps {
                script {
                    // Ensure the sh step is within a node block
                    sh 'docker build -t hakimedy/flaskapp:$BUILD_NUMBER .'
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    // Ensure the sh step is within a node block
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    // Ensure the sh step is within a node block
                    sh 'docker push hakimedy/flaskapp:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            script {
                // Ensure the sh step is within a node block
                sh 'docker logout'
            }
        }
    }
}
