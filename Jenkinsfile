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
        stage('Run Tests') {
            steps {
                script {
                // Assuming your Docker image name is "${REGISTRY}/${DOCKER_LABEL_PRODUCT}:${VERSION}"
                sh("""docker run jayrath17/my-fastapi-app:latest pytest tests/""")
                }
            }
            }
        stage('Pytest Tests'){
            steps {
                script {
                    docker.image("my-fastapi-app:${env.BUILD_NUMBER}").inside("--entrypoint=''"){
                        sh '''#!/bin/bash
                           echo "Running Tests!"
                           pytest
                           '''
                    }
                }
            }
        }
        stage('Publish Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'a5aa7a09-e16d-402d-b06e-35b1deaa4d54') {
                        docker.image("jayrath17/my-fastapi-app:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
}
