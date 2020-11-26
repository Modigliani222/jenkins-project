#!groovy
// Run docker build
 
 pipeline {
     agent {
          label 'master'
          }
     stages {
         stage("create docker image") {
             steps {
                  echo " ============== start building image ============="
                  dir ('images') {
                           sh 'docker build . '
                  }
             } 
           }
     // Running Dccker container
    stage('Docker Run') {
        steps{
            script {
          dockerImage.run("-p 8181:8080  --rm --name mezey ucun")
      }
   }
 }
}
}


     
         
