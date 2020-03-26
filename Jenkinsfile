pipeline {
   agent any

   stages {
      stage('Prepare') {
         steps {
            kubernetesDeploy(kubeconfigId:'mykubeconfig')
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