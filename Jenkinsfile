pipeline {
	environment {
    registry = "docker_hub_account/repository_name"
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
                 app = docker.build("underwater:${env.BUILD_NUMBER}")
                }
            }
        }
		
	 stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
	
  }
  
  
  }
