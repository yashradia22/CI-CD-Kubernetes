pipeline {
    agent any
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/yashradia22/CI-CD-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn clean package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp 76988/cloudhedge_registry:latest'
                //sh 'docker tag samplewebapp 76988/cloudhedge_registry:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push 76988/cloudhedge_registry:latest'
        //  sh  'docker push 76988/cloudhedge_registry:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8000:8080 76988/cloudhedge_registry"
 
            }
        }
    }
	}
    
