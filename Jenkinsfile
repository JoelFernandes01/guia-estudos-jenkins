pipeline {                                                                                                        
  agent any

    stages {
      stage('Build Docker Image'){
        steps {
          script {
            dockerapp = docker.build("joelfernandes01/guia-jenkins:${env.BUILD.ID}", '-f ./src/Dockerfile ./src')
                  }                                                                                        
        }                                                                                                                                                                                                                   
      }
    }
}