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
                           sh 'docker build -t zekushka/v01  . '
                  }
             } 
}
}
}              
