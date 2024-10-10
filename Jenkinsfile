pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "your-dockerhub-repo/your-app:latest"  // Replace with your Docker Hub repository
        ARGOCD_APP = "your-argo-app"                            // Replace with your ArgoCD application name
        K3S_NAMESPACE = "default"                               // Set your desired Kubernetes namespace
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Simulanis-Dev-ShivaKumar/node.git'  // Updated GitHub repository URL
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
        stage('Create Kubernetes Manifests') {
            steps {
                script {
                    sh '''
                    cat <<EOF > deployment.yaml
                    apiVersion: apps/v1
                    kind: Deployment
                    metadata:
                      name: your-app                                    // Replace with your actual app name
                    spec:
                      replicas: 2
                      selector:
                        matchLabels:
                          app: your-app                                // Replace with your actual app name
                      template:
                        metadata:
                          labels:
                            app: your-app                              // Replace with your actual app name
                        spec:
                          containers:
                          - name: your-app                              // Replace with your actual app name
                            image: ${DOCKER_IMAGE}
                            ports:
                            - containerPort: 3000
                    EOF
                    '''
                }
            }
        }
        stage('Deploy with ArgoCD') {
            steps {
                script {
                    sh '''
                    argocd app create ${ARGOCD_APP} \
                      --repo https://github.com/Simulanis-Dev-ShivaKumar/node.git \  // Updated GitHub repository URL
                      --path ./ \                                      // Adjust path if necessary
                      --dest-server https://k3s-cluster \             // Replace with your K3s cluster server URL
                      --dest-namespace ${K3S_NAMESPACE}
                    argocd app sync ${ARGOCD_APP}
                    '''
                }
            }
        }
    }
}
