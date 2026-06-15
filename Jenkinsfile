pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Unnati206/JenkinsSpringboot.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t springbootdemoapp .
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop springbootdemoapp || true
                docker rm springbootdemoapp || true

                docker run -d \
                --name springbootdemoapp \
                -p 8080:8080 \
                springbootdemoapp
                '''
            }
        }
    }
}