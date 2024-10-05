pipeline {
    agent any

    environment {
        PROJECT_ID = 'sound-inn-437705-m4'
        CLUSTER_NAME = 'autopilot-cluster-1'
        ZONE = 'us-central1-c'
        DOCKER_IMAGE = "us-central1-docker.pkg.dev/sound-inn-437705-m4/image/nginx"
    }

    stages {
        stage('Deploy to GKE') {
            steps {
                script {
                    // Get credentials for the GKE cluster
                    sh "gcloud container clusters get-credentials autopilot-cluster-1 --region us-central1 --project sound-inn-437705-m4"

                    // Deploy the application
                    sh """
                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml
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
