pipeline {
    agent any

    environment {
        IMAGE_NAME = 'assignment-image'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/arshiya406/Assignment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(IMAGE_NAME)
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name assignment-container ${IMAGE_NAME}'
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh 'curl --fail http://localhost:5000'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment successful!'
            }
        }
    }

    post {
        always {
            sh 'docker stop assignment-container || true'
            sh 'docker rm assignment-container || true'
        }
    }
}
