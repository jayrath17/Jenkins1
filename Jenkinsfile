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
                    docker.withRegistry('docker.io', 'a5aa7a09-e16d-402d-b06e-35b1deaa4d54') {
                        docker.image("my-fastapi-app:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
}
