pipeline {
   agent any

   stages {
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