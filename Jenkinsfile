pipeline {
    agent any

    environment {
        IMAGE_NAME = 'helloworld-htmlimage'
        IMAGE_TAG = 'v1'
        DOCKER_REPO = '16p124manoj/dockerhtmlrepo'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "the checkout stage "
                git branch: 'main', credentialsId: 'mygithubcredentials', url: 'https://github.com/ManojkumarKamaraj/htmlimage.git'
                echo 'get the repo from branch'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "the build running  stage "
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                    echo "build stage was succeeded"
                }
            }
        }

        stage('login to docker'){
            steps{
                script{
                    echo "pushing docker image to docker hub"
                    withCredentials([usernamePassword(credentialsId: 'jenkins-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        sh 'echo "$jenkins-credentials" | docker login -u "$DOCKER_USER" --password-stdin'
                    }
                }
                    echo "pushing docker credential"
                }
            }
        }

        stage('push to docker-hub'){
            steps{
                script {
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }


        stage('Cleanup') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
