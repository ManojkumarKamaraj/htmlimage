pipeline {
    agent any

    environment {
        IMAGE_NAME = 'helloworld-htmlimage'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "the checkout stage "
                git branch: 'main', credentialsId: 'mygithubcredentials', url: 'https://github.com/ManojkumarKamaraj/htmlimage.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "the build running  stage "
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        // Optional: Push to DockerHub or private registry
        /*
        stage('Push Image') {
            steps {
                withDockerRegistry([credentialsId: 'your-dockerhub-creds', url: '']) {
                    script {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
        */

        stage('Cleanup') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
