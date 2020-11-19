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
              sh '''	    
              
               customImage = docker.build(registry + ":${BUILD_NUMBER}")
              '''
      	    }  
          }

      stage('Push image' ) {
         steps {
            echo 'Pushing image to Dockerhub...'
	    sh '''
              docker.withRegistry('', 'registryCredential') {
	          customImage.push()
		 
	       }
              '''
      	   }  
        }
     }  
  }
