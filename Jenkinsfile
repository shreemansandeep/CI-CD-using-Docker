pipeline {
    agent any
	
//	  tools
  //  {
  //     maven "Maven"
  //  }
 stages {
      stage('Git checkout') {
           steps {
             
                git credentialsId: 'GitCred', url: 'https://github.com/shreemansandeep/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Maven Build') {
           steps {
             
                sh 'mvn clean package'             
          }
        }
        

  stage('Docker Build image and Tag') {
           steps {
              
                sh 'docker build -t dockersandheep/samplewebapp:latest .' 
               // sh 'docker tag samplewebapp dockersandheep/samplewebapp:latest'
               // sh 'docker tag samplewebapp dockersandheep/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Push image to Docker Hub') {
          
            steps {
      //   withDockerRegistry([ credentialsId: "DockerHub", url: "" ]) {
      //    sh  'docker push dockersandheep/samplewebapp:latest'
        //  sh  'docker push dockersandheep/samplewebapp:$BUILD_NUMBER' 
     //   }
                 sh 'docker login -u dockersandheep -p Docker@66'
		 dh 'docker push dockersandheep/samplewebapp:latest'
          }
        }
     
      stage('Run Docker container') {
             
            steps 
			{
                sh "docker run -d -p 8002:8080 dockersandheep/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://ubuntu@172.31.34.167 run -d -p 8002:8080 dockersandheep/samplewebapp"  
 
            }
        }
    }  
	}
    
