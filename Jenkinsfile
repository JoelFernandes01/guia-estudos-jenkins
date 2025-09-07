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
         
         stage('Push Docker Image'){
             steps {
               script {
                 docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                     dockerapp.push('latest')
                     dockerapp.push("${env.BUILD.ID}")
                }
               }
             } 
         }
 
#       stage('Deploy no Kubernetes'){
#         steps {
#           sh 'echo "Executando o comando kubectl appy"'
#         }
#       }
     }
   }
