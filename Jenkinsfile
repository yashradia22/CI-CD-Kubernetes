pipeline {
    agent any
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/yashradia22/CI-CD-Kubernetes.git'
             
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
                sh 'docker tag samplewebapp yashdevopsmay/devops-batch:latest'
                //sh 'docker tag samplewebapp 76988/cloudhedge_registry:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push yashdevopsmay/devops-batch:latest'
        //  sh  'docker push 76988/cloudhedge_registry:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Deploy to Kubernetes') {
    steps {
        script {
            sh 'kubectl apply -f deployments.yml'
            
        }
    }
}

    }
	}
