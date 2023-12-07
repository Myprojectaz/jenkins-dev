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

		stage('package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}

		 stage('Build and Push Docker Image') {
    		  environment {
       			DOCKER_IMAGE = "yaswanth98/heyone:${BUILD_NUMBER}"
        // DOCKERFILE_LOCATION = "java-maven-sonar-argocd-helm-k8s/spring-boot-app/Dockerfile"
        		REGISTRY_CREDENTIALS = credentials('docker-cred')
      }
      steps {
        script {
            sh 'docker build -t ${DOCKER_IMAGE} .'
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                dockerImage.push()
            }
        }
      }

	}

	post {
		always {
			echo 'im awesome. i run always'
		}
		success {
			echo 'i run when you are successful'
		}
		failure {
			echo 'i run when you fail'
		}
	}
}
