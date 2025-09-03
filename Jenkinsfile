pipeline {
    agent any

    environment {
        IMAGE_NAME = 'helloworld-htmlimage'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'checkout the project...'
                git branch: 'main', credentialsId: 'mygithubcredentials', url: 'https://github.com/ManojkumarKamaraj/htmlimage.git'
                echo 'get the repo from branch'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "building image"
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
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
