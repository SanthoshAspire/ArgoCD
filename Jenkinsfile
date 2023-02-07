pipeline {
	environment {
    registry = "sanosh9183/testing"
    registryCredential = 'dockerhub'     
    DOCKERHUB_CREDENTIALS= credentials('dockerhubcredentials')  
	NEXUS_VERSION = "nexus3"
    NEXUS_PROTOCOL = "http"
    NEXUS_URL = "13.232.247.176:8081"
    NEXUS_REPOSITORY = "argocd-image-helm"
    NEXUS_CREDENTIAL_ID = "Nexus_Cred"
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
					//sh "cd /home/ubuntu/Demo/Argo_Project"
					sh "sudo docker build -t sanosh9183/testing:${env.BUILD_NUMBER} ."
					//sh "sudo docker build . -t 52.66.41.87:8081/argocd-image-helm/:${env.BUILD_NUMBER}"
					//sh "sudo docker push -a sanosh9183/testing:${env.BUILD_NUMBER} http://52.66.41.87:9001/repository/argocd-image-helm/"
					sh "sudo docker push sanosh9183/testing:${env.BUILD_NUMBER}"
					//sh "sudo docker push sanosh9183/testing:${env.BUILD_NUMBER} http://52.66.41.87:8081/repository/argocd-image-helm/"
					sh "echo printing the images"
					sh "sudo docker images"
					
					sh "sudo docker tag sanosh9183/testing:${env.BUILD_NUMBER} 52.66.41.87:8081/repository/argocd-image-helm/sanosh9183/testing:${env.BUILD_NUMBER}"
					sh "echo printing the tagged images"
					sh "sudo docker images"
					//(working)sh "docker push 52.66.41.87:8081/repository/argocd-image-helm/sanosh9183/testing:${env.BUILD_NUMBER}"
					sh "docker login -u admin -p admin http://52.66.41.87:8081/repository/argocd-image-helm/"
					sh "docker push http://52.66.41.87:8081/repository/argocd-image-helm/52.66.41.87:8081/repository/argocd-image-helm/sanosh9183/testing:${env.BUILD_NUMBER}"
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
	//stage('Login-Into-Docker') {
      //steps {
		// script{
				//sh "logging into docker"
				//sh "sudo docker login -u sanosh9183 -p Kiran@9183"
				//sh "logged in successfully"
				 //sh "sudo chmod 777 /var/run/docker.sock"
			 	//sh "permission enabled"
				//sh "sudo docker login -u sanosh9183 -p Kiran@9183"
			 	//sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				//sh "echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"              		
			//	echo "Login Completed"
				
		 
		// }
		
	  
        //container('docker') {
	    //  sh "sudo docker login -u sanosh9183 -p Kiran@9183"
		//sh "logged in successfully"
     // }
    //}
    //}	
	
	  // stage('Push-Images-Docker-to-DockerHub') {
     // steps {
       // container('docker') {
       //   sh "sudo docker push sanosh9183/testing-image:${env.BUILD_NUMBER}"
     // }
   // }
 //    }
	stage('Push image to Nexus') {
			steps{
				script{
					sh "docker login -u admin -p admin http://52.66.41.87:9001/repository/argocd-image-helm/"
					sh "login success"
					//sh "sudo docker push 52.66.41.87:9001/repository/argocd-image-helm/"
					//app.push("${env.BUILD_NUMBER}")
					//sh "sudo docker push sanosh9183/testing-image:${env.BUILD_NUMBER}"
					
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
