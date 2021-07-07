pipeline {
   agent any
  tools {
      // Install the Maven version configured as "M3" and add it to the path.
	  jdk 'java8'
      maven "Maven-3.3.9"
   }
   stages
   {
   stage('checkout') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/164411Prathyusha/Prat-game-of-life.git'
        }
        
        }
   }
}
