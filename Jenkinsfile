pipeline {
    agent {
        node {
            label 'jenkinsagent'
        }      
    }
	
    environment {
        START_PIPELINE = 'YES'  // YES or NO
        NEWTAG = ''
    }
	
    stages {
	
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }
        }	
		
        stage("Checkout from SCM"){
            steps {
               git branch: 'master', credentialsId: 'meghachandsingh', url: 'https://gitlab.com/meghachandsingh/ipl_project'
            }
        }
        } 
		

    }
}


