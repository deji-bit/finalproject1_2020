pipeline {
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
              cd finalproject1_2020/
               app = docker.build ("appimage001")
            '''
      	    }  
          }

      stage('Push image' ) {
         steps {
            echo 'Pushing image to Dockerhub...'
	    sh '''
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
	          app.push("${env.BUILD_NUMBER}")
		  app.push("latest")
	       }
              '''
      	   }  
        }
     }  
  }
