pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dbell799/ci-cd-pipeline-using-aws-jenkins-docker'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'e89ddf3a-33d3-42f1-ad37-76a90e39a6ba') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}

