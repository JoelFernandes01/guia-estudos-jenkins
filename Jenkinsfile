pipeline {                                                                                                                                                                                         
  1     agent any
  2 
  3     stages {
  4         stage('Build Docker Image'){
  5             steps {
  6                 script {
  7                     dockerapp = docker.build("JoelFernandes01/guia-estudos-jenkins:${env.BUILD.ID}", '-f ./src/Dockerfile ./src')
  8                 }
  9             }  
 10         }
 11         
 12         stage('Push Docker Image'){
 13             steps {
 14               script {
 15                 docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
 16                     dockerapp.push('latest')
 17                     dockerapp.push("${env.BUILD.ID}")
 18                }
 19               }
 20             } 
 21         }
 22 
 23       stage('Deploy no Kubernetes'){
 24         steps {
 25           sh 'echo "Executando o comando kubectl appy"'
 26         }
 27       }
 28     }
 29   }
