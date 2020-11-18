### Upon code commit by the developer, the pipeline will perform the following actions:
### 1. establish the ip of the box which is passive
### 2. build a new image of the application
### 3. deploy a new containerised version of the application pointing to the same redis box


pipeline {
   agent any

   stages {
     stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	      sh '''
             sudo ssh -o StrictHostKeychecking=no -i /home/ec2-user/first-keys ec2-user@172.31.5.213 '
            git clone https://github.com/deji-bit/finalproject1_2020.git /home/ec2-user/appcode'
            '''
      	 }  
       }
      stage('Deploy' ) {
         steps {
            echo 'Deploying app to Passive box'
	      sh '''
	         sudo ssh -i /home/ec2-user/first-keys ec2-user@172.31.5.213 '
	           cd /home/ec2-user/appcode/
	         docker build -t appimage001 .
	       docker rm -f appdeployment || 'true'
	     docker run -d -p 80:80 -e REDIS=172.31.4.187 -e REDIS_PORT=6379  -e REDIS_PWD=redis --name appdeployment appimage001 '
            '''
      	 }
       }
      stage('Cleanup' ) {
         steps {
            echo 'Removing used files and folders'
	      sh '''
                sudo ssh -i /home/ec2-user/first-keys ec2-user@172.31.5.213 '
	        sudo rm -rf /home/ec2-user/appcode/ '
            '''
      	 }
       }
    }  
}
