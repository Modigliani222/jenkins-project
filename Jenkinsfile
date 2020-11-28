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
     stage("run docker image") {
        steps { 
            script {   
                    dockerImage.run("-p 8181:5000 --rm --name zeynalovContainer")

 
        }
     }
  }
} 
}             
