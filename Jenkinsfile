pipeline {
   agent any

   stages {
      stage('Prepare') {
         steps {
            sh 'pwd'
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