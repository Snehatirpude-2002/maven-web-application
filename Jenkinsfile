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
            withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                sh 'mvn sonar:sonar -Dsonar.projectKey=maven-web-application -Dsonar.token=$SONAR_TOKEN'
            }
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
				withCredentials([usernamePassword(credentialsId: 'nexus',
												  usernameVariable: 'admin',
												  passwordVariable: 'admin123',)]) {
								sh 'mvn deploy -s /var/lib/jenkins/.m2/settings.xml'
								}
								}
								}
								}
}
								
								
