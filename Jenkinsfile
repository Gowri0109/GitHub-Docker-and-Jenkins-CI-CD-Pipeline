pipeline {
    agent any
    
    stages {
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Gowri0109/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t adomicarts/nodeapp-cuban:${BUILD_NUMBER} .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'samin-docker', variable: 'samindocker')]) {
                    script {  
                        sh "docker login -u adomicarts -p '${samindocker}'"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                sh "docker push adomicarts/nodeapp-cuban:${BUILD_NUMBER}"
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
