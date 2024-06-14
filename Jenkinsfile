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
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {  
                build job: "Fortify_Scan_Job",propagate: true,wait: true,
                parameters: [
                      [$class: 'StringParameterValue', name: 'name', value: "sidd"],
                      [$class: 'StringParameterValue', name: 'tagname', value: "${Scan_value1}"],
                            ]
              }
            }
        }

        stage('Blackduck Scan') {
            when {
                expression { env.Blackduck_scan == 'YES'}
            }

            steps {
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                build job: "Blackduck_Scan_Job",propagate: true,wait: true,
                parameters: [
                      [$class: 'StringParameterValue', name: 'name', value: "sidd"],
                      [$class: 'StringParameterValue', name: 'tagname', value: "${Scan_value2}"],
                            ]
              }
                  }
        }

        stage('ZAP Scan') {
            when {
                expression { env.ZAP_scan == 'NO'}
            }

            steps {
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                build job: "zap_Scan_Job",propagate: true,wait: true,
                parameters: [
                      [$class: 'StringParameterValue', name: 'name', value: "sidd"],
                      [$class: 'StringParameterValue', name: 'tagname', value: "${Scan_value3}"],
                            ]
              }
            }
        }

        stage('Deploy') {
            when {
                expression { env.START_Deploy == 'YES'}
            }

            steps {
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                build job: "Deployment",propagate: true,wait: true,
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

