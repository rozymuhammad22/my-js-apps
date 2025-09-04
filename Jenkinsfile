pipeline {
    agent any

    environment {
        APP_NAME = "jenkins-ui-demo"
        PORT = "3000"
    }

    triggers {
        githubPush()   // otomatis trigger saat ada push dari GitHub webhook
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/<username>/jenkins-docker-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${APP_NAME}:latest ."
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    // stop container lama jika ada
                    sh """
                    if [ \$(docker ps -q -f name=${APP_NAME}) ]; then
                        docker stop ${APP_NAME} && docker rm ${APP_NAME}
                    fi
                    """
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh "docker run -d --name ${APP_NAME} -p ${PORT}:3000 ${APP_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment sukses, buka http://<IP-server>:${PORT}"
        }
        failure {
            echo "❌ Build/Deployment gagal, cek log di Jenkins console."
        }
    }
}

