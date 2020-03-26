pipeline {
   agent any

   stages {
      stage('Prepare') {
         steps {
            kubernetesDeploy(kubeconfigId:'mykubeconfig', configs:'deployment.yaml')
            sh 'kubectl get pod'
         }
      }
      stage('Build') {
         steps {
            sh 'kubectl version --client'
         }
      }
      stage('Deploy') {
         steps {
            echo 'Hello Gooner'
         }
      }

   }
}