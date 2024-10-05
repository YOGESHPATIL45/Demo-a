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
                    // Set the project in gcloud
                    sh "gcloud config set project ${PROJECT_ID}"
                    
                    // Get credentials for the GKE cluster
                    sh "gcloud container clusters get-credentials ${CLUSTER_NAME} --zone ${REGION}"
                    
                    // Optionally, add deployment steps here, e.g., deploying your Docker image
                    // sh "kubectl apply -f deployment.yaml" // Uncomment and adjust as necessary
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
