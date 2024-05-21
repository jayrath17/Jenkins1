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
                    docker.withRegistry('', 'jayrath17') {
                        docker.image("my-fastapi-app:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
}
