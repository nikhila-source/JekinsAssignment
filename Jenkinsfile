#!groovy

def call() {
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
				checkout scm
			}
			stage ('Build ${ARTIFACTID} and ${VERSION}') {
				steps {
					script {
					
					sh "mvn clean install"
					
					}
				}
			}
         	stage ('Awaiting for approval for deploying ${ARTIFACTID} and ${VERSION}') {
				steps {
					script {
						timeout(time: 300, unit: 'SECONDS') {
						input 'Are you ready to deploy?'
						}
					}
				}
			}
          
          	stage ('Deploying ${ARTIFACTID} and ${VERSION}') {
				steps {
					script {
						sh "Here ssh into EC2 instance and deploy to tomcat."
						sh "I'm skipping this, since I dont have instance ready"
					}
				}
			}
		}
	}  	
}
