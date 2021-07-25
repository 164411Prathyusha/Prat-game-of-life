pipeline {
   agent any
	 environment {

      sonar_url = 'http://172.31.4.216:9000/'
      sonar_username = 'admin'
      sonar_password = 'admin'
      nexusUrl = '172.31.12.54:8081'
      artifact_version = '0.0.1'

 }
  tools {
      // Install the Maven version configured as "M3" and add it to the path.
	  jdk 'Java8'
      maven "Maven_3.3.9"
   }
   stages
   {
   stage('checkout') {
         steps {
            // Get some code from a GitHub repository
            git branch: 'main', url: 'https://github.com/164411Prathyusha/Prat-game-of-life.git'
        }
        
        }
	   stage ('Compile and Build') {
         steps {
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
}