pipeline {

agent any
 environment {
     PROJECT_ID = 'jenkins'
     CLUSTER_NAME = 'minikube'
     dockerimagename = 'samheutmaker/node-app'
 }
 stages {
     stage("Checkout code") {
         steps {
             checkout scm
         }
     }
     stage("Build image") {
         steps {
             script {
                 dockerImage = docker.build dockerimagename
             }
         }
     }
     stage("Push image") {
        environment {
               registryCredential = 'dockerhub-credentials'
           }
         steps {
             script {
                 docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
                    dockerImage.push("latest")
                 }
             }
         }
     }

 stage("Deploy Kubernetes") {

     steps {
       sh "kubectl apply -f deployment.yml"
       sh "kubectl apply -f service.yml"
       }                
     }

   }
 }

 

