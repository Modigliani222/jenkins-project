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
                           sh 'docker build -t zekushka/v02  . '
                  }
             } 
            }
         stage("run docke image") {
           steps {   
         echo " =========== Running a docker image that we've just created"
                    sh 'docker run  -d -p 8181:8080  zekushka/v02'
 
}
}
}
}              
