pipeline {
   agent any

   stages {
     stage('Polling SCM' ) {
         steps {
            echo 'Cloning code from repository'
	      sh '''
             git clone https://github.com/deji-bit/finalproject1_2020.git
	     pwd
	    sudo scp -o StrictHostKeychecking=no -i /home/ec2-user/first-keys -rf finalproject1_2020/ ec2-user@172.31.5.213:/tmp
	    pwd
            '''
      	 }  
       }
    }  
}
