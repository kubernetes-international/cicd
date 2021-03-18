node{
    checkout scm
    stage('Deploy Staging') {
        withKubeConfig([credentialsId: '9a088633-e7d2-462b-bfb2-bb1e86b51af2', serverUrl: 'https://35.224.254.59']) {
            sh 'kubectl config view'
            sh 'kubectl get po'
        }
    }   
}