pipeline {
    agent any
    environment {
        PROJECT_ID = 'fourth-memento-307608'
        CLUSTER_NAME = 'cluster-1'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'gke-admin'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        // stage("Build image") {
        //     steps {
        //         script {
        //             myapp = docker.build("DOCKER-HUB-USERNAME/hello:${env.BUILD_ID}")
        //         }
        //     }
        // }
        // stage("Push image") {
        //     steps {
        //         script {
        //             docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
        //                     myapp.push("latest")
        //                     myapp.push("${env.BUILD_ID}")
        //             }
        //         }
        //     }
        // }        
        stage('Deploy to GKE') {
            steps{
                withCredentials([file(credentialsId: 'gke-admin', variable: 'GC_KEY')]) {
                    sh("""  gcloud auth activate-service-account --key-file="${GC_KEY}" && \
                            gcloud config set project "${PROJECT_ID}" && \
                            gcloud config set container/cluster "${CLUSTER_NAME}" && \
                            gcloud config set compute/zone "${LOCATION}" && \
                            gcloud container clusters get-credentials "${GKE_CLUSTER_NAME}" --zone "${GKE_CLUSTER_ZONE}" && \
                            kubectl get po""")
                    sh("echo 'test2' && kubectl get po")
                }
            }
        }
    }    
}