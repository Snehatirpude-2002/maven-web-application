pipeline {
	agent any
	stages {
		stage('build and deploy') {
			steps { 
				withCredentials([usernamePassword(credentialsId: 'nexus',
												  usernameVariable: 'admin',
												  passwordVariable: 'admin123')]) {
					sh 'mvn clean deploy -s /var/lib/jenkins/.m2/settings.xml'
				}
			}
		}
	}
}
