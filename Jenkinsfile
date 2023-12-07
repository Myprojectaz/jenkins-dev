pipeline {
    agent any

    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"
        DOCKER_USERNAME = 'Yaswanth98'
        DOCKER_PASSWORD = 'Yashu@1998'
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
            steps {
                script {
                    def DOCKER_IMAGE = "yaswanth98/heyone:${BUILD_NUMBER}"

                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    sh "docker build -t ${DOCKER_IMAGE} ."
                    sh "docker push ${DOCKER_IMAGE}"
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
