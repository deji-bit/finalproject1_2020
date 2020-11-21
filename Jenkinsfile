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

      stage('Deploy App' ) {
         steps {
            echo 'Deploying app to Passive box'
	      sh '''
	         sudo ssh -i first-keys ec2-user@172.31.5.213 '
	       sudo docker rm -f popularityvote || "true"
	     sudo docker run -d -p 80:80 -e REDIS=172.31.4.187 -e REDIS_PORT=6379  -e REDIS_PWD=redis --name popularityvote dejidock01/myprojectsappimage '
            '''
      	 }
       }

	   
      stage('Cleanup' ) {
         steps {
            echo 'Removing used files and folders'
	      sh '''
	        sudo rm -rf finalproject1_2020/ || 'true'
            '''
      	 }
       }    
   }
}
