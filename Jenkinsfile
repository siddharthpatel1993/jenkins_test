pipeline {
    agent {
        node {
            label 'jenkinsagent'
        }      
    }
	
    environment {
        START_PIPELINE = 'Yes'  // YES or NO
        NEWTAG = ''
    }
	
    stages {
        stage('Generate Tag') {
            when {
                expression { env.START_PIPELINE == 'YES'}
            }
            steps {
                script {
                    sh 'mkdir GENERATE-TAG'
                    sh 'cd GENERATE-TAG'
                    sh 'pwd'
                }
            }
        } 
    }
}
