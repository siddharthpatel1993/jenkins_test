//added one comment
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
	
    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '2', 
                    numToKeepStr: '2'
            )
    }
	
    stages {
		
        stage("Checkout from SCM"){
            when {
                expression { env.START_PIPELINE == 'YES'}
            }
            steps {
               git branch: 'master', credentialsId: 'meghachandsingh', url: 'https://gitlab.com/meghachandsingh/ipl_project'
            }
        }

        stage('Job Starts here') {
            when {
                expression { env.START_PIPELINE == 'YES'}
            }

            steps {
                build job: "Test_slow_track",propagate: true,wait: true,
                parameters: [
                 [$class: 'StringParameterValue', name: 'DEVICE_BUILD_VERSION', value: "VERSION_TO_TEST"],
                 [$class: 'StringParameterValue', name: 'JOB_TO_RUN', value: "SI_fc_slow_track"],
                 [$class: 'StringParameterValue', name: 'TRACK_RESULT_NAME', value: "QA_Track"],
                 [$class: 'StringParameterValue', name: 'TRACK_RESULT_ID', value: "BUILD_NUMBER"],
                 [$class: 'StringParameterValue', name: 'EDGE_TAGS', value: "dev,qa"],
                            ]
                  }

              }                

         }

    post {
     always {
            echo 'I will get displayed always'
        }

        success {
            echo 'I will get displayed if job is success'
        }

        failure {
            echo 'I will get displayed if job is failure'
        }
    }
}


