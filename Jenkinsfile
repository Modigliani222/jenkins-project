#!groovy
// Run docker build
 
 pipeline {
     environment {
     registry = "zeynalov/jenkins-project"
     registryCredential = 'docker-hub'
     dockerImage = 'zekushka'
     }
     agent {
          label 'master'
          }
     stages {
         stage('Cloning our Git') {
           steps {
             git 'https://github.com/Modigliani222/jenkins-project.git'
                           
                  }
             } 
            }
         stage('Building our image') {
           steps{
            script {
              dockerImage = docker.build registry + ":$BUILD_NUMBER"
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
