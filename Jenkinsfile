pipeline {
    agent any
	   environment 
	   {
		  sonar_url = 'http://172.31.4.216:9000/'
		  sonar_username = 'admin'
		  sonar_password = 'admin'
		  nexusUrl = '172.31.4.216:8081'
		  artifact_version = '0.0.1'

        }
    tools 
	{
		  // Install the Maven version configured as "M3" and add it to the path.
		  jdk 'Java8'
		  maven "Maven_3.3.9"
    }
	
	stages
    {
        stage('checkout') 
		{
          steps 
		  {
				// Get some code from a GitHub repository
				git branch: 'main', url: 'https://github.com/164411Prathyusha/Prat-game-of-life.git'
          }
        
        }
	    stage ('Compile and Build') 
		{
			 steps 
			 {
				   sh '''
				   mvn clean install -U  -Dmaven.test.skip=true 
				   '''
             }
	    }
	    
	     stage ('Docker Build') {
         steps {
	 withAWS(credentials:'jenkins'){
            // withCredentials([usernamePassword(credentialsId: 'JenkinsDeploymentUser', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) 
           sh '''
	   aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 781939683518.dkr.ecr.us-east-2.amazonaws.com
          docker build -t 781939683518.dkr.ecr.us-east-2.amazonaws.com/docker:latest . 
	  
           '''
	   }
         }
	}
	   
	   stage ('Docker image publish to ECR') {
         steps {
           sh '''
	  docker push 781939683518.dkr.ecr.us-east-2.amazonaws.com/docker:latest
	  
           '''
         }
			 
    }
}
