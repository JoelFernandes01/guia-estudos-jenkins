pipeline {                                                                                                        
  agent any

    stages {
      stage('Build Docker Image'){
        steps {
          script {
            dockerapp = docker.build("joelfernandes7/guia-jenkins:${env.BUILD.ID}", '-f ./src/Dockerfile ./src')
          }                                                                                        
          sh 'echo "Executando o comando Docker Build"'                                            
        }                                                                                                         
      }                                                                                                           
                                                                                                                  
    stage('Push Docker Image'){                                                                                   
      steps {
        sh 'echo "Executando o comando Docker push"'
      }
    }

    stage('Deploy no Kubernetes'){
      steps {
        sh 'echo "Executando o comando kubectl appy"'
      }
    }
  }
}
