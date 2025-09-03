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


        stage('Cleanup') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
