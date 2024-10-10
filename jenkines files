pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "your-dockerhub-repo/your-app:latest"
        ARGOCD_APP = "your-argo-app"
        K3S_NAMESPACE = "default"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR-REPO-HERE.git'
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
                      name: your-app
                    spec:
                      replicas: 2
                      selector:
                        matchLabels:
                          app: your-app
                      template:
                        metadata:
                          labels:
                            app: your-app
                        spec:
                          containers:
                          - name: your-app
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
                      --repo https://github.com/YOUR-REPO-HERE.git \
                      --path / \
                      --dest-server https://k3s-cluster \
                      --dest-namespace ${K3S_NAMESPACE}
                    argocd app sync ${ARGOCD_APP}
                    '''
                }
            }
        }
    }
}
