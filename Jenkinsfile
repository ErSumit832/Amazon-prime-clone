pipeline {
    agent any

    environment {
        DOCKER_IMAGE_FRONTEND = 'amazon-prime-frontend'
        DOCKER_IMAGE_BACKEND = 'amazon-prime-backend'
        DOCKER_REGISTRY = 'localhost:5000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ErSumit832/Amazon-prime-clone.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_FRONTEND}", "-f Dockerfile.frontend .")
                    docker.build("${DOCKER_IMAGE_BACKEND}", "-f Dockerfile.backend .")
                }
            }
        }

        stage('Run Containers') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    // Add your testing commands here
                    echo 'Running tests...'
                }
            }
        }

        stage('Stop Containers') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml down'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

