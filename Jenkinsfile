pipeline{
    agent{
        label 'master'
    }
    stages{
        stage('Deploy Patient App') {
        steps {
            withCredentials([
                string(credentialsId: 'minikube', variable: 'api_token')
                ]) {
                    sh 'kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true apply -f httpd.yaml'
                }
            }
        }
    }
}