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
                    sh 'gcloud config set project $PROJECT_ID'
                    sh 'gcloud container clusters get-credentials $ CLUSTER_NAME --zone $REGION'
                    
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
