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
    }
}
