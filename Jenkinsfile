pipeline {
   agent any

   stages {
     stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	      sh '''
	      pwd
              git clone https://github.com/deji-bit/finalproject1_2020.git 
	      sudo cp -rf finalproject1_2020/ /home/ec2-user/
	     cd /home/ec2-user
	     pwd
	    ssh -o StrictHostKeychecking=no -i first-keys ec2-user@172.31.5.213 '
	    sudo mkdir test123
	    pwd
	    '
	    pwd
            '''
      	 }  
       }
    }  
}
