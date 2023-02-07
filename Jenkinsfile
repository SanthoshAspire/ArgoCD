pipeline {
	environment {
    registry = "sanosh9183/testing"
    registryCredential = 'dockerhub'
  }
  
  agent any
  
  stages {
   	stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
	
	stage('Build') { 
			steps {
				script{
					sh 'docker build -t sanosh9183/testing:latest .'
				}
      	
      }
	
	
	
            //steps { 
            //    script{
            //     app = docker.build("registry:${env.BUILD_NUMBER}")
            //   }
            //}
        }
		
	stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
	stage('Push image to Nexus') {
			steps{
				script{
					sh 'docker login -u admin -p admin http://13.232.247.176:8081/repository/argocd-image-helm/'
					app.push("${env.BUILD_NUMBER}")
				
				}
			
			}
	
	
        
    }
	stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('https://720766170633.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
					}
				}
            }
	}  
  
  }

}
