pipeline {
	agent any

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"
		

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
	}
}
		/*
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
				sh "mvn failsafe:integration-test failsafe:verify"
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
        			//withCredentials([usernamePassword(credentialsId: 'yaswanth98', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                		//def dockerHubCredentials = docker.registryCredentials('https://hub.docker.com')
					docker.withRegistry('', 'dockerhub'){
                // Login to Docker Hub using --password-stdin
                		//sh "echo ${dockerHubCredentials.secretPassword} | docker login --username ${dockerHubCredentials.secretUsername} --password-stdin"

                // Push Docker image
                		dockerImage.push()
                		dockerImage.push('latest')
					}
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