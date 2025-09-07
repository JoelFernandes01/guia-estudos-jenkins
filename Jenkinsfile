pipeline {                                                                                                        
  agent any

    stages {
      stage('Build Docker Image'){
        steps {
          script {
            dockerapp = docker.build("joelfernandes7/guia-jenkins:${env.BUILD.ID}", '-f ./src/Dockerfile ./src')
                  }                                                                                        
        }                                                                                                                                                                                                                   
      }
    }
}