pipeline {
    agent any

    environment {
        PROJECT_ID = 'sound-inn-437705-m4'
        CLUSTER_NAME = 'autopilot-cluster-1'
        CLUSTER_REGION =  'us-central1' // Specify your GCP region
        IMAGE_NAME = 'us-central1-docker.pkg.dev/sound-inn-437705-m4/image/nginx' // Specify the existing image
        GCP_CREDENTIALS = credentials('gcp-service-account') // GCP service account credentials
    }

    stages {
        stage('Authenticate to GCP') {
            steps {
                // Authenticate to Google Cloud with service account credentials
                withCredentials([file(credentialsId: 'gcp-service-account', variable: 'GCP_KEYFILE')]) {
                    sh 'gcloud auth activate-service-account --key-file=$GCP_KEYFILE'
                }
            }
        }

        stage('Connect to GKE Cluster') {
            steps {
                // Configure kubectl to use the target GKE cluster with region
                sh "gcloud container clusters get-credentials $CLUSTER_NAME --region $CLUSTER_REGION --project $PROJECT_ID"
            }
        }

        stage('Deploy to GKE') {
            steps {
                // Deploy the Nginx container to GKE
                sh """
                kubectl create deployment nginx-app --image=$IMAGE_NAME || \
                kubectl set image deployment/nginx-app nginx-app=$IMAGE_NAME
                """
                
                // Expose the Nginx deployment as a service (NodePort)
                sh 'kubectl expose deployment nginx-app --type=NodePort --port=80 || true'
            }
        }
    }
}
