pipeline {
    agent any

    environment {
        PROJECT_ID = 'sound-inn-437705-m4'
        CLUSTER_NAME = 'autopilot-cluster-1'
        REGION = 'us-central1'
        DOCKER_IMAGE = "us-central1-docker.pkg.dev/sound-inn-437705-m4/image/nginx"
    }

    stages {
        stage('Deploy to GKE') {
            steps {
                script {
                    sh 'gcloud config set project $GKE_PROJECT'
                    sh 'gcloud container clusters get-credentials $GKE_CLUSTER --zone $GKE_ZONE'
                    
                    // Apply Kubernetes manifests (assumes you have a deployment.yaml file)
                    sh 'kubectl apply -f k8s/deployment.yaml'
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
