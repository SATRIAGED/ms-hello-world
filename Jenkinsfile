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
 stage("Deploy Kubernetes") {

     steps {
        container('kubectl') {
            sh 'kubectl apply -f deployment.yml'
            sh 'kubectl apply -f service.yml'
          }
        }
       //kubernetesDeploy(configs: "deployment.yml", "service.yml")
       }                
     }

   }
 }

