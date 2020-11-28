#!groovy
// Run docker build
 
 pipeline {
     environment {
     registry = "zeynalov/jenkins-project"
     registryCredential = 'docker-hub'
     dockerImage = ''
     }
     agent {
          label 'master'
          }
     stages {
         stage("Buil a docker image") {
             steps {
             script {
                  echo " ============== start building image ============="
                  dir ('images') {
                      dockerImage = docker.build("zekushka")
    
                           
                  }
             } 
            }
    }
     stage('Deploy our image') { 

            steps { 

                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push()
        
           
              
              
             }
           }
        }
     } 
     stage("run docker image") {
        steps {   
            echo " =========== Running a docker image that we've just created"
                    sh 'docker run  -d -p 8181:8080  zekushka'
 
        }
     }
  }
}              
