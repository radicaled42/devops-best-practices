# Jenkins Sample

```json
pipeline {
    agent any

    environment {
        // Define your environment variables here
        REGISTRY = "your-docker-registry"  // e.g., Docker Hub or another container registry
        IMAGE_NAME = "your-app-image"      // Image name for the Docker image
        KUBE_CONFIG_PATH = "/path/to/kubeconfig" // Path to kubeconfig on the Jenkins agent
        NAMESPACE = "your-k8s-namespace"   // Kubernetes namespace to deploy
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm // Checkout the repository from SCM
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://your-registry-url', 'docker-credentials-id') {
                        docker.image("${REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Use kubectl to apply the Kubernetes manifest, assuming it’s available in your repository
                    withKubeConfig([credentialsId: 'k8s-credentials-id', kubeconfig: "${KUBE_CONFIG_PATH}"]) {
                        sh """
                        kubectl set image deployment/your-app-deployment your-container=${REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER} -n ${NAMESPACE}
                        kubectl rollout status deployment/your-app-deployment -n ${NAMESPACE}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean up the workspace after the build
        }
    }
}
```