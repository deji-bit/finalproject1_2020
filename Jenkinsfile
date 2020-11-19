pipeline {
   agent any

   stages {
     stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	      sh '''
	      pwd
              git clone https://github.com/deji-bit/finalproject1_2020.git 
	      
	     
	    pwd
	    ssh -o StrictHostKeychecking=no -i first-keys ec2-user@172.31.5.213 '
	    sudo mkdir test123
	    pwd
	    '
	    pwd
	    sudo scp -v -o StrictHostKeyChecking=no -i first-keys -rf finalproject1_2020/ ec2-user@172.31.5.213:/tmp
	    pwd
            '''
      	 }  
       }
    }  
}
