pipeline{
    agent{
        label 'local'
    }
    parameters {
       choice(name: 'ENVIRONMENT', choices: ['am-dev','am-int'], description: 'Select the Environment to Deploy configstore,amster,openam. Default am-dev')
    }
    options{
        timeout(time: 20, unit: 'MINUTES')
    }
    stages{
        stage('Cleanup'){
            steps{
                echo "******Deployment To ******* ${params.ENVIRONMENT}"
                withCredentials([
                string(credentialsId: 'minikube', variable: 'api_token')
                ]) {
                    sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true 
                        delete deploy httpd-deploy -n ${params.ENVIRONMENT}"
                }
            }
        }
        stage('Deploy httpd') {
        steps {
            withCredentials([
                string(credentialsId: 'minikube', variable: 'api_token')
                ]) {
                    sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true apply -f httpd.yaml"
                }
            }
        }
    }
}