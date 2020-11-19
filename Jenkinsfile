pipeline {
   environment {
       registry = "dejidock01/myprojects"
           registryCredential = 'dockerhub'
        customImage = ''
    }	
   agent any

   stages {
      stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	       sh '''
	          pwd
                  git clone https://github.com/deji-bit/finalproject1_2020.git
                '''
          }
       }
	  
      stage('Build image' ) {
         steps {
            echo 'Building image from Dockerfile...'
	       script { 	    
                  customImage = docker.build(registry + "appimage:${BUILD_NUMBER}")
              }
      	  }  
       }

      stage('Push image' ) {
         steps {
            echo 'Pushing image to Dockerhub...'
	       script {
                  docker.withRegistry('', registryCredential) {
	            customImage.push()
                }
             }  
          }
       }  
       stage('Remove unused Docker Image') {
	  steps {
		  sh "docker rmi $registry + appimage:$BUILD_NUMBER" || true
	   }   
       }
    }
}
