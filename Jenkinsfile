node{
    checkout scm
    stage('Deploy Staging') {
        withKubeCredentials([credentialsId: 'jenkins-robot', serverUrl: 'https://35.224.254.59']) {
            sh 'kubectl config view'
            sh 'kubectl get po'
        }
    }   
}