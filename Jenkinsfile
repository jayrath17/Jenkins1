pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-fastapi-app:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Publish Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://dockerhub.com', 'dockerhub_credentials') {
                        docker.image("my-fastapi-app:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
}
