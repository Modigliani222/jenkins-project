#!groovy
// Run docker build
      def buildNumber = BUILD_NUMBER
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
                      dockerImage = docker.build registry + ":$buildNumber" 
    
                           
                  }
             } 
            }
    }

     stage('Push to the DockerHub') { 

           steps { 

             script { 
                  docker.withRegistry( '', registryCredential ) { 
                      dockerImage.push()
        
           
              
              
            }
          }
       }
     } 
      
     stage("Pull and Run a Docker image on the deployment server") {
         
       steps {
         sshagent(['Docker-Dev-Server']) {
             sh "ssh -o StrictHostKeyChecking=no ssd@192.168.1.237 docker rm -f zeynalovcontainer || true "
            
             sh "ssh -o StrictHostKeyChecking=no ssd@192.168.1.237 docker run -d -p 8181:8080 --name zeynalovcontainer zeynalov/jenkins-project:${builNumber}"
         }
 }
        

 
        }
     }
  }
