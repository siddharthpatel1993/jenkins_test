pipeline{
    agent any

    environment {
        APP_NAME = "DCUBE_APP"
        APP_ENV  = "DEV"
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '1', 
                    numToKeepStr: '1'
            )
    }

    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps {
               git branch: 'master', credentialsId: 'github_credential', url: 'https://github.com/siddharthpatel1993/jenkins_test'
            }
        }

        stage("Running Shell script") {
            steps {
                script {
                        sh "set fileformat=unix"
                        sh "echo 'Performing Build'"
                }
            }
        }
    }
}
