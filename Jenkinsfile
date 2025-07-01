pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dbell799/ci-cd-pipeline-using-aws-jenkins-docker'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'e89ddf3a-33d3-42f1-ad37-76a90e39a6ba') {
                        docker.image(env.DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh '''
                    docker rm -f my-flask-app || true
                    docker pull ${DOCKER_IMAGE}:latest
                    docker run -d --name my-flask-app -p 5000:5000 ${DOCKER_IMAGE}:latest
                    '''
                }
            }
        }
    }
}
