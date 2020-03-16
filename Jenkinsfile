#!groovy

//def call() {
	pipeline {
		agent any
      	tools {
			maven 'Maven'
			jdk 'Java'
		}
      	environment {
		ARTIFACTID = readMavenPom().getArtifactId()
		VERSION = readMavenPom().getVersion()
		}
		stages {
			stage ('Checkout Source Code') {
				steps {
					
					
					git branch: 'develop', url: 'https://github.com/nikhila-source/JekinsAssignment.git'
					
					
				}
			}
			stage ("Build ${ARTIFACTID} and ${VERSION}") {
				steps {
					script {
					
					sh "mvn clean install"
					
					}
				}
			}
         	stage ("Awaiting for approval for deploying ${ARTIFACTID} and ${VERSION}") {
				steps {
					script {
						timeout(time: 300, unit: 'SECONDS') {
						input 'Are you ready to deploy?'
						}
					}
				}
			}
          
          	stage ("Deploying ${ARTIFACTID} and ${VERSION}") {
				steps {
					script {
						echo "Here I dont have available EC2 right now."
						echo "So, deploying into local tomcat"
						sh "cp ${WORKSPACE}/target/JenkinsAssignment.war /opt/apache-tomcat-8.0.32/webapps/"
					}
				}
			}
		}
	}  	
//}
