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
                // Build your Docker image here
            }
        }
        stage('Push Docker Image') {
            steps {
                // Push your Docker image here
            }
        }
        stage('Create Kubernetes Manifests') {
            steps {
                // Create Kubernetes manifests here
            }
        }
        stage('Deploy with ArgoCD') {
            steps {
                // Deploy your application using ArgoCD here
            }
        }
    }
}
