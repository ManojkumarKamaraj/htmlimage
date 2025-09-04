pipeline {
    agent any

    environment 
    {
        IMAGE_NAME = '16p124manoj/dockerhtmlrepo'
        IMAGE_TAG = 'v1'
    }

    stages 
    {
        stage('Checkout') 
        {
            steps 
            {
                echo "the checkout stage "
                git branch: 'main', credentialsId: 'mygithubcredentials', url: 'https://github.com/ManojkumarKamaraj/htmlimage.git'
                echo 'get the repo from branch'
            }
        }

        stage('Build Docker Image') 
        {
            steps 
            {
                script 
                {
                    echo "the build running  stage "
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                    echo "build stage was succeeded"
                }
            }
        }

        stage('login to docker')
        {
            steps
            {
                script
                {
                    echo "logging into docker hub with same repository name"
                    withCredentials([usernamePassword(credentialsId: 'jenkins-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) 
                    {
                    script 
                    {
                        sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    }

                    }
                    echo "logged with docker credentials"
                }
            }
        }

        stage('push to docker-hub')
        {
            steps
            {
                script
                {
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage('Cleanup') 
        {
            steps 
            {
                sh 'docker image prune -f'
            }
        }
    } // stages end

}
