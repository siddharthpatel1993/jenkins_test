pipeline{
    agent any

    environment {
        APP_NAME = "DCUBE_APP"
        APP_ENV  = "Java"
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
                        sh "echo 'Performing ${APP_NAME} Build'"
                }
            }
        }

        stage("Test") {
            parallel {
                stage("Java Execution") {
                     when {
                      environment(name: "APP_ENV", value: "Java")
                     }   
                    steps {
                        sh "echo 'Java'"
                    }
                }
                stage("PRE") {
                     when {
                      environment(name: "APP_ENV", value: "Java1")
                     }

                    steps {
                        sh "./deploy.sh pre"
                    }
                }
                stage("PROD") {
                     when {
                      environment(name: "APP_ENV", value: "Java2")
                     }

                    steps {
                        sh "./deploy.sh prod"
                    }
                }
            }
        }
    }
}
