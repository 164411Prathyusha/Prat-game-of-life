pipeline {
    agent any
	   environment 
	   {
		  sonar_url = 'http://34.68.82.31:9000/'
		  sonar_username = 'admin'
		  sonar_password = 'admin'
		  nexusUrl = '34.68.82.31:8081'
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
	    stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('sonarqube') {
           sh '''
           mvn clean package org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=false
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" -Dsonar.sourceEncoding=UTF-8
           '''
                 }
           }
	    }
	    
	    stage ('Publishing Artifact') {
	steps {
	nexusArtifactUploader artifacts: [[artifactId:'gameoflife', classifier: '', file: '/var/lib/jenkins/workspace/firstpipeline/gameoflife-build/target/gameoflife-build-1.0-SNAPSHOT.jar', type:'jar', type: 'jar']], credentialsId: '33e7a578-b459-4beb-b5c7-b7e5ac957e70', groupId: 'com.wakaleo.gameoflife', nexusUrl: '10.128.0.6:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'deploy', version: '4.0.0'
           archiveArtifacts '**/*.jar'
	
	
	}
	}
	  stage ('Docker build')
{  
     steps
 {
    sh '''
       docker build -t 164411/game-of-life-jenkins:v1 .
       '''
     }
}
    stage('Push docker image')
    {
        steps
   {
     sh '''
       docker login --username 164411 --password 1205@Ramya
       docker push 164411/game-of-life-jenkins:v1
      '''
        }  
    }
}
}
