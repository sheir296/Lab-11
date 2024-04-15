pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Use credentials for Git authentication
                git credentialsId: '4367b485-f77a-4e69-a812-38e4924eccb0', url: 'https://github.com/sheir296/Lab-11.git'
            }
        }
        
        stage('Dependency Installation') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t lab-11 .'
            }
        }
        
        stage('Run Docker Image') {
            steps {
                sh 'docker run -d -p 8080:80 lab-11'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                // Use Docker Hub credentials for authentication
                withCredentials([usernamePassword(credentialsId: '4367b485-f77a-4e69-a812-38e4924eccb0', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push lab-11'
                }
            }
        }
    }
}
