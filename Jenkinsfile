pipeline {
	agent any
	tools {
		maven 'maven9.10'
	}
	stages {
		stage('build') {
		steps { 
			sh 'mvn clean package'
		}
		}
		stage('sonarqube analysis') {
			steps {
				withSonarQubeEnv('sonarqube server') {
					sh 'mvn sonar:sonar Dsonar.projectKey=maven-web-application -Dsonar.login=squ_959e3af9bfc0c8b57d945ae9d6628134b14608e2'
				}
			}
		}
		stage('quality gate') {
			steps {
				timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
				}
			}
		}
		stage('deploy to nexus') {
			steps {
				withCredentials([usernamePassword(credentialId: 'nexus',
												  usernameVariable: 'admin',
												  passwordVariable: 'admin123',)]) {
								sh 'mvn deploy -s /var/lib/jenkins/.m2/settings.xml'
								}
								}
								}
								}
}
								
								
