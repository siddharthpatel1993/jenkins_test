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

        stage('Tag Calulation') {
            when {
                expression { env.START_PIPELINE == 'YES'}
            }
            steps {
                script {
                    // Get the latest tag year
                    def tagyear = sh(script: "git describe --tags --abbrev=0 | grep -o 'R.*' | cut -d'.' -f 2 | sort -n -r | head -1", returnStdout:true).trim()
                    sh "echo Latest Tag year: $tagyear"

                    // Get the latest PI number
                    def tagpinumber = sh(script: "git describe --tags --abbrev=0 | grep -o 'R.*' | cut -d'.' -f 3 | sort -n -r | head -1", returnStdout:true).trim()
                    sh "echo Latest tag PI number: $tagpinumber"

                    // Get the latest tag build number
                    def tagbuildnum = sh(script: "git describe --tags --abbrev=0 | grep -o 'R.*' | cut -d'.' -f 4 | sort -n -r | head -1", returnStdout: true).trim()
                    sh "echo Latest tag buildnumber: $tagbuildnum"

                    // Remove leading zeros from the build number
                    tagbuildnum = sh(script: "expr $tagbuildnum + 0", returnStdout: true).trim()
                    sh "echo $tagbuildnum"

                    // Increment build number
                    tagbuildnum = sh(script: "expr $tagbuildnum + 1", returnStdout: true).trim()
                    sh "echo $tagbuildnum"

                    // Prepare the 4 digit build number format
                    tagbuildnum = sh(script: "printf '%04i' $tagbuildnum", returnStdout: true).trim()
                    sh "echo $tagbuildnum"

                    // New tag for this latest build
                    NEWTAG = "R.$tagyear.$tagpinumber.$tagbuildnum"
                    sh "echo New tag: ${NEWTAG}"
                }            
            }
        }

        stage('Creating tar file') {
            when {
                expression { env.START_PIPELINE == 'YES'}
            }

            steps {
                script {

                  sh "echo New tag: ${NEWTAG}"
                  def JobParameters = [
                      string(name: 'name', value: 'sidd'),
                      string(name: 'tagname', value: "${NEWTAG}")
                  ]
                
                  def BUILD = build job: 'childJob', 
                  parameters: JobParameters,
                  propogate: true,
                  wait: true
            }
        }
      }

        stage("Cleanup Workspace"){
            when {
                expression { env.START_PIPELINE == 'YES'}
            }
            steps {
                cleanWs()
            }
        }
		
    }
}


