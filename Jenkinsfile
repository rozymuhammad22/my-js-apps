pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/<username>/jenkins-docker-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t my-js-apps .'
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    sh 'docker run --rm my-js-apps'
                }
            }
        }
    }
}
