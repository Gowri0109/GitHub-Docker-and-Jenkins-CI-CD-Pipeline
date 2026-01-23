pipeline {
    agent any

    stages {

        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main',
                        url: 'https://github.com/Gowri0109/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t gowrisuresh0109/nodeapp-cuban:${BUILD_NUMBER} ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'samin-docker',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                      echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push gowrisuresh0109/nodeapp-cuban:${BUILD_NUMBER}"
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
