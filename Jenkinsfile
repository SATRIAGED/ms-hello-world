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
        sh "sed -i 's/node-app:latest/node-app:${env.BUILD_ID}/g' deployment.yml"
                 script {
     withKubeConfig([credentialsId: 'kubeconfig']) 
         {
       sh "kubectl apply -f deployment.yml --validate=false"
       sh "kubectl apply -f service.yml"
       }                
     }
       //kubernetesDeploy(configs: "deployment.yml", "service.yml")
       }                
     }

   }
 }

