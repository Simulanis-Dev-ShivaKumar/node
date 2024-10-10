pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout from the specified branch
                git branch: 'main', credentialsId: 'gitcred', url: 'https://github.com/Simulanis-Dev-ShivaKumar/node.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Example build command
                sh 'echo "Building Docker Image..."'
                // Add your actual Docker build command here
                // sh 'docker build -t your-image-name .'
            }
        }
        stage('Push Docker Image') {
            steps {
                // Example push command
                sh 'echo "Pushing Docker Image..."'
                // Add your actual Docker push command here
                // sh 'docker push your-image-name'
            }
        }
        stage('Create Kubernetes Manifests') {
            steps {
                // Example command for creating Kubernetes manifests
                sh 'echo "Creating Kubernetes Manifests..."'
                // Add your actual command for creating manifests here
            }
        }
        stage('Deploy with ArgoCD') {
            steps {
                // Example command for deploying with ArgoCD
                sh 'echo "Deploying with ArgoCD..."'
                // Add your actual command for deployment here
            }
        }
    }
}
