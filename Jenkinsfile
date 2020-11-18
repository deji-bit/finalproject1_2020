pipeline {
   agent any

   stages {
     stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	      sh '''
             git clone https://github.com/deji-bit/finalproject1_2020.git || true
	     pwd
	    sudo scp -o StrictHostKeychecking=no -rf -i /home/ec2-user/first-keys finalproject1_2020/ ec2-user@172.31.5.213:/tmp
            '''
      	 }  
       }
      stage('Deploy' ) {
         steps {
            echo 'Deploying app to Passive box'
	      sh '''
	         sudo ssh -i /home/ec2-user/first-keys ec2-user@172.31.5.213 '
	           cd /tmp/finalproject1_2020/
	         docker build -t appimage001 .
	       docker rm -f appdeployment || "true"
	     docker run -d -p 80:80 -e REDIS=172.31.4.187 -e REDIS_PORT=6379  -e REDIS_PWD=redis --name appdeployment appimage001 '
            '''
      	 }
       }
      stage('Cleanup' ) {
         steps {
            echo 'Removing used files and folders'
	      sh '''
                sudo ssh -i /home/ec2-user/first-keys ec2-user@172.31.5.213 '
	        sudo rm -rf /tmp/finalproject1_2020/ '
            '''
      	 }
       }
    }  
}
