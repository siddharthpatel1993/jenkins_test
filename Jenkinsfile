//added one comment
pipeline {
    agent {
        node {
            label 'jenkinsagent'
        }
    }

    environment {
        Fortify_scan = 'YES' // YES or NO
        Blackduck_scan = 'YES' // YES or NO
        ZAP_scan = 'YES' // YES or NO
        START_Deploy = 'YES' // YES or NO

        Scan_value1 = 'Fortify Scan'
        Scan_value2 = 'Blackduck Scan'
        Scan_value3 = 'ZAP Scan'
    }

    options {
        buildDiscarder logRotator(
                    daysToKeepStr: '2',
                    numToKeepStr: '2'
            )
    }

    stages {

        stage('Fortify Scan') {
            when {
                expression { env.Fortify_scan == 'YES'}
            }

            steps {
                build job: "Fortify_Scan_Job",propagate: true,wait: true,
                parameters: [
                      [$class: 'StringParameterValue', name: 'name', value: "sidd"],
                      [$class: 'StringParameterValue', name: 'tagname', value: "${Scan_value1}"],
                            ]
                  }
            }
    }       


    post {
     always {
           echo "Clean after the job is completed"
           cleanWs()
        }

        success {
            echo 'I will get displayed if job is success'
        }

        failure {
            echo 'I will get displayed if job is failure'
        }
    }
}

