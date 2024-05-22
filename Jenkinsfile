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
        stage('Pytest Tests'){
            steps {
                script {
                    docker.image("my-fastapi-app:${env.BUILD_NUMBER}").inside("--entrypoint=''"){
                        sh '''#!/bin/bash
                            echo "docker images!"
                           docker images
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
