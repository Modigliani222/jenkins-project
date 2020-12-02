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
                      dockerImage = docker.build registry 
    
                           
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
      
     stage("Deploy  docker image in Docker Deployment Server") {
         
       steps {
         sshagent(['Docker-Dev-Server']) {
             sh "ssh -o StrictHostKeyChecking=no root@192.168.1.237 docker rm -f zeynalovcontainer || true "
            
             sh "ssh -o StrictHostKeyChecking=no root@192.168.1.237 docker run -d -p 8181:8080 --name zeynalovcontainer zeynalov/jenkins-project:latest"
         }
 }
        

 
        }
     }
  }
