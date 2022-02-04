//DECLARATIVE
pipeline {
	agent any

	environment { 
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('checkout') {
			steps {
				sh 'mnv --version'
				sh 'docker version'
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		stage('compile') {
			steps{
				sh "mvn clean compile"
			}
		}
        stage ('test') {
			steps{
				sh "mvn test"
			}
		}         
		stage ('integration test') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		}
	}	
}	