// def appName = 'web-app'
// def namespace = 'web'


pipeline {

agent { Dockerfile true }
 stages {
     stage("Checkout code") {
         steps {
             checkout scm
         }
     }
     stage('Git clone') {
      steps {
        git branch: 'main', credentialsId: 'usnmepswdGIT',
          url: 'https://github.com/SATRIAGED/ms-hello-world.git'
      }
    }
     stage("Build image") {
         steps {
             sh 'npm version'
             sh 'docker image list'
         }
     }
 stage("Deploy Kubernetes") {
    // when {
    //   branch 'main'
    // }
     steps {
      withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'kubeconfig', namespace: 'default', restrictKubeConfigAccess: false, serverUrl: 'https://192.168.0.26:6443') {
      // sh 'kubectl apply -f deployment.yaml'
      // sh 'kubectl apply -f service.yaml'
    //   sh "mkdir -p ~/.kube/"
      sh "kubectl apply -f deployment.yml"
      sh "kubectl apply -f service.yml"
    // some block
      }
      // withKubeConfig([credentialsId: 'kubeconfig']) {
      //     sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
      //     sh 'kubectl apply -f service.yaml'
      //   }
        // kubernetesDeploy(
        //   kubeconfigId: 'kubeconfig',
        //   configs: 'deployment.yaml',
        //   enableConfigSubstitution: true
        // )
        // kubernetesDeploy(
        //   kubeconfigId: 'kubeconfig',
        //   configs: 'service.yaml',
        //   enableConfigSubstitution: true
        // )
        // kubeconfig(caCertificate: 'kubecertif', credentialsId: 'kubeconfig', serverUrl: 'https://192.168.0.26:6443') {
        //   sh "kubectl apply -f deployment.yaml"
        //   sh "kubectl apply -f service.yaml"
          // kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        //}
      //    {
      //  sh "kubectl apply -f deployment.yaml"
      //  sh "kubectl apply -f service.yaml"
      //  }                
       //kubernetesDeploy(configs: "deployment.yml", "service.yml")
       }                
     }

   }
 }
