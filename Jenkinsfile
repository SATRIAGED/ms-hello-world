def appName = 'ms-hello-world'
def namespace = 'web'


pipeline {

agent any
 environment {
     dockerimagename = 'jenkins/jnlp-slave'
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

