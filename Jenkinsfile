pipeline {
    agent any
    environment {
        PROJECT_ID = 'fourth-memento-307608'
        CLUSTER_NAME = 'cluster-1'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'gke-admin'
        NAMESPACE = 'default'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage('Deploy to GKE') {
            steps{
                withCredentials([file(credentialsId: 'gke-admin', variable: 'GC_KEY')]) {
                    sh("""  gcloud auth activate-service-account --key-file="${GC_KEY}" && \
                            gcloud config set project "${PROJECT_ID}" && \
                            gcloud config set container/cluster "${CLUSTER_NAME}" && \
                            gcloud config set compute/zone "${LOCATION}" && \
                            gcloud container clusters get-credentials "${CLUSTER_NAME}" --zone "${LOCATION}" 
                        """)
                    sh("cat ms1/deployment.yaml | envsubst | kubectl apply -f - ")
                    sh("cat ms1/service.yaml | envsubst | kubectl apply -f - ")
                }
            }
        }
    }    
}