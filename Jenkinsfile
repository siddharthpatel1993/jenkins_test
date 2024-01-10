pipeline{
    agent any

    environment {
        componentType = "Tomcat"
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '1', 
                    numToKeepStr: '1'
            )
    }

    parameters {
        //booleanParam(name: "RELEASE", defaultValue: false)
        choice(name: "component_type", choices: ["Java", "Apache", "Tomcat"])
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
                        sh "echo 'Performing ${componentType} Build'"
                }
            }
        }

        stage("Performing Build") {
            parallel {
                stage("Java Build") {
                    when { expression { params.component_type == "Java" } }
                    steps {
                        sh "echo 'Java Build'"
                    }
                }
                stage("Apache Build") {
                    when { expression { params.component_type == "Apache" } }
                    steps {
                        sh "echo 'Apache Build'"
                    }
                }
                stage("Tomcat Build") {
                    when { expression { params.component_type == "Tomcat" } }
                    steps {
                        sh "echo 'Tomcat Build'"
                    }
                }
            }
        }
    }
}
