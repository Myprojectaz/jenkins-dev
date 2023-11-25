pipeline {
	agent any

	environment {
		dockerHome = tool 'myDocker'
		PATH = /opt/maven/apache-maven-3.9.5/bin:PATH
		PATH = "$dockerHome/bin:$PATH"

	}

	stages {
		stage('checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "build"
				echo "PATH - PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"

			}
		}

		stage('compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failesafe:verify"
			}
		}

	
		stage('package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}


		stage('Build Docker image') {
			steps {
				script {
					dockerimage = docker.build("yaswanth98/regapp:${env.BUILD_TAG}")
					
				}
			}
		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dcokerImage.push('latest');
					}
				}
			}
		}
	}

	post {
		always {
			echo 'im awesome. i run always'
		}
		success {
			echo 'i run when you are succesfull'
		}
		failure {
			echo 'i run when you fail'
		}
	}
		
	
}
