pipeline{
    agent any

    environment {
        componentType = "java"
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
                      environment(name: "componentType", value: "Java")
                     }   
                    steps {
                        sh "echo 'Java'"
                    }
                }
                stage("Apache Execution") {
                     when {
                      environment(name: "componentType", value: "Apache")
                     }

                    steps {
                        sh "echo 'Apache'"
                    }
                }
                stage("Tomcat Execution") {
                     when {
                      environment(name: "componentType", value: "Tomcat")
                     }

                    steps {
                        sh "echo Tomcat'"
                    }
                }
            }
        }
    }
}
