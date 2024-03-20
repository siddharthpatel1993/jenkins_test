//added one comment
pipeline {
    agent {
        node {
            label 'jenkinsagent'
        }      
    }
	
    environment {
        START_PIPELINE = 'YES' // YES or NO
        Fortify_scan = 'YES' // YES or NO
        Blackduck_scan = 'YES' // YES or NO
        ZAP_scan = 'YES' // YES or NO
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

        stage('Fortify Scan') {
            when {
                expression { env.Fortify_scan == 'NO'}
            }
            steps {
                script {
                    sh "echo Scan"
                }            
            }
        }

        stage('Blackduck Scan') {
            when {
                expression { env.Blackduck_scan == 'NO'}
            }

            steps {
                script {

                  sh "echo scan"
                  //def JobParameters = [
                      //string(name: 'name', value: 'sidd'),
                      //string(name: 'tagname', value: "${NEWTAG}")
                  //]
                
                  //def BUILD = build job: 'childJob1', 
                  //parameters: JobParameters,
                  //propogate: true,
                  //wait: true
            }
        }
      }

        stage('ZAP Scan') {
            when {
                expression { env.ZAP_scan == 'NO'}
            }

            steps {
                script {

                  sh "echo New"
                  //def JobParameters = [
                      //string(name: 'name', value: 'sidd'),
                      //string(name: 'tagname', value: "${NEWTAG}")
                  //]

                  //def BUILD = build job: 'childJob2',
                  //parameters: JobParameters,
                  //propogate: true,
                  //wait: true
            }
        }
      }


        //stage('Commented section') {
            //when {
                //expression { env.START_PIPELINE == 'YES'}
            //}

            //steps {
                //script {

                  //sh "echo New tag: ${NEWTAG}"
                  //def JobParameters = [
                      //string(name: 'name', value: 'sidd'),
                      //string(name: 'tagname', value: "${NEWTAG}")
                  //]

                  //def BUILD = build job: 'childJob3',
                  //parameters: JobParameters,
                  //propogate: true,
                  //wait: true
            //}
        //}
      //}

        //stage('Job Starts here') {
            //when {
                //expression { env.START_PIPELINE == 'YES'}
            //}

            //steps {
                //build job: "Test_slow_track",propagate: true,wait: true,
                //parameters: [
                 //[$class: 'StringParameterValue', name: 'DEVICE_BUILD_VERSION', value: "VERSION_TO_TEST"],
                 //[$class: 'StringParameterValue', name: 'JOB_TO_RUN', value: "SI_fc_slow_track"],
                 //[$class: 'StringParameterValue', name: 'TRACK_RESULT_NAME', value: "QA_Track"],
                 //[$class: 'StringParameterValue', name: 'TRACK_RESULT_ID', value: "BUILD_NUMBER"],
                 //[$class: 'StringParameterValue', name: 'EDGE_TAGS', value: "dev,qa"],
                            //]
                  //}

              //}                

        stage("Cleanup Workspace"){
            when {
                expression { env.START_PIPELINE == 'YES'}
            }
            steps {
                cleanWs()
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


