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
			stage ('Build '{env.ARTIFACTID}' and '{env.VERSION}'') {
				steps {
					script {
						echo "${ARTIFACTID} ${VERSION}"
					sh "mvn clean install"
					
					}
				}
			}
         	stage ('Awaiting for approval for deploying ${env.ARTIFACTID} and ${env.VERSION}') {
				steps {
					script {
						timeout(time: 300, unit: 'SECONDS') {
						input 'Are you ready to deploy?'
						}
					}
				}
			}
          
          	stage ('Deploying ${env.ARTIFACTID} and ${env.VERSION}') {
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
