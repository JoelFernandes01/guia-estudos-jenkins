pipeline {
    agent any

    environment {
        REGISTRY = "joelfernandes01"
        IMAGE = "guia-jenkins"
        TAG = "latest"
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
  }
}
