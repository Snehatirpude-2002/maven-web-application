pipeline {
	agent any
	tools {
		maven 'maven9.10'
		git 'Default'
	}
	Stages{
		stage('gitcheckout'){
			steps{
				git branch: 'main', url:https:'//github.com/Snehatirpude-2002/maven-web-application.git'
			}
		}
		stage('mavenBuild'){
			steps{
				sh "mvn clean package"
			}
			)
			stage('sonarAnalysis'){
				steps{
					sh "mvn sonar:sonar"
				}
			}
			stage('nexusUpload'){
				steps{
					sh "mvn deploy"
				}
			}
		}
	}
