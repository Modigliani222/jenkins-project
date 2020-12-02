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
         sshagent(['Ubuntu-EC2-PEM-KEY']) {
             sh "ssh -o StrictHostKeyChecking=no ubuntu@3.101.104.59 docker rm -f zeynalovcontainer || true "
            
             sh "ssh -o StrictHostKeyChecking=no ubuntu@3.101.104.59  docker run -d -p 8080:8080 --name zeynalovcontainer zeynalov/jenkins-project:${buildNumber}"
         }
 }
        

 
        }
     }
  }
