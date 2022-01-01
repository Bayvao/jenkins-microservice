pipeline {
	agent any
	
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		
		registryCredentials = "nexus"
        registry = "http://35.245.176.217:8081/"
        dockerImage = ''
		
		 // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "127.0.0.1:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "nexus-release"
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
		
		stage('package'){
			steps{
				sh "mvn clean install -DskipTests"
			}
		}
		
		stage('Docker Image Build'){
			steps{
				//"docker build -t bayvao/jenkins-microservice"$env.BUILD_TAG
				
				script{
					dockerImage = docker.build("bayvao/jenkins-microservice:${env.BUILD_TAG}")
				}
			}
		}
		
		stage('Docker Image Deploy to Nexus') {
			steps{  
				script {
					docker.withRegistry(registry, registryCredentials) {
						dockerImage.push('latest');
					}
				}
			}
		}		
	}
}
