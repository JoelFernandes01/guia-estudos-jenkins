pipeline {
 17   agent any
 16 
 15     stages {
 14       stage('Build Docker Image'){
 13         steps {
 12           sh 'echo "Executando o comando Docker Build"'
 11         }
 10       }
  9 
  8     stage('Push Docker Image'){
  7       steps {
  6         sh 'echo "Executando o comando Docker push"'
  5       }
  4     }
  3 
  2     stage('Deploy no Kubernetes'){
  1       steps {
19          sh 'echo "Executando o comando kubectl appy"'                                                                                                                                              
  1       }
  2     }
  3   }
  4 }
