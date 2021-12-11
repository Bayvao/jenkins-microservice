pipeline {
	agent any
	
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	
	stages {
		stage('Build'){
			steps{
				sh 'mvn --version'
				sh 'docker version'
				
				echo "Build"
				echo "$PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.BUILD_TAG"
				echo "BUILD URL - $env.BUILD_URL"
			}
		}
	}
	
}
