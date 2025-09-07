pipeline {
    agent any

    environment {
        REGISTRY = "joelfernandes01"
        IMAGE    = "guia-jenkins"
        TAG      = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh '''
                            echo ">>> Logando no DockerHub..."
                            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin

                            echo ">>> Construindo imagem Docker..."
                            docker build -t $REGISTRY/$IMAGE:$TAG ./src
                        '''
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh '''
                        echo ">>> Enviando imagem para o DockerHub..."
                        docker push $REGISTRY/$IMAGE:$TAG
                    '''
                }
            }
        }

        stage('Deploy NGINX via Docker Compose') {
            steps {
                script {
                    // Cria um docker-compose temporário no workspace
                    writeFile file: 'docker-compose.yml', text: """
version: '3'
services:
  nginx:
    image: nginx:latest
    container_name: nginx_jenkins
    ports:
      - "8081:80"
    restart: always
"""

                    // Executa o docker-compose
                    sh '''
                        echo ">>> Rodando NGINX via Docker Compose..."
                        docker compose down || true
                        docker compose up -d
                        docker ps
                    '''
                }
            }
        }
    }
}
