pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-static-website'
    }

    stages {

        stage('Test') {
            steps {
                echo 'Checking Application files'

                sh 'test -f index.html'
                sh 'test -f style.css'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'

                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing Docker Image to Docker Hub...'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag ${IMAGE_NAME}:${BUILD_NUMBER} $DOCKER_USER/${IMAGE_NAME}:${BUILD_NUMBER}
                        docker push $DOCKER_USER/${IMAGE_NAME}:${BUILD_NUMBER}
                    '''
                }
            }
        }

    }

    post {
        always {
            sh 'docker logout || true'
        }
    }
}