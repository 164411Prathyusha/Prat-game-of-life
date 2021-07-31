pipeline {
   agent any
  tools {
      // Install the Maven version configured as "M3" and add it to the path.
	  jdk 'Java8'
      maven "Maven_3.3.9"
   }
   stages
   {
   stage('git clone') {
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
   }
}
