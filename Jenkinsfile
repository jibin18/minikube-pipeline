pipeline{
    agent{
        label 'local'
    }
    parameters {
       choice(name: 'ENVIRONMENT', choices: ['am-dev','default'], description: 'Select the Environment to Deploy configstore,amster,openam. Default am-dev')
    }
    options{
        timeout(time: 20, unit: 'MINUTES')
    }
    stages{
        stage('Delete configmap'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'minikube', variable: 'api_token')]){
                        //getConfigMap="kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}"
                        //sh "kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}"
                        
                        configMapName = sh (
                        script: "kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}",returnStdout: true).trim()                       
                        echo "configmap: ${configMapName}"
                        
                        if(configMapName=="configmap/httpd-cm")
                        {
                            echo 'test passed !!! '
                            sh "kubectl delete configmap/httpd-cm --force -n ${params.ENVIRONMENT}"                                                         
                        }
                        

                       
                        //    command  = "kubectl delete configmap "+""+configMapNames[i].replace( 'configmap/', '' ).trim()+""+" -n "+${params.ENVIRONMENT}+" --grace-period=0 --force"                                    
                    }
                }
            }
        }
        stage('Cleanup'){
            steps{
                echo "******Deployment To ******* ${params.ENVIRONMENT}"
                withCredentials([
                string(credentialsId: 'minikube', variable: 'api_token')
                ]) {
                    //sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true delete deploy httpd-deploy -n ${params.ENVIRONMENT}"
                    sh "kubectl --token $api_token --insecure-skip-tls-verify=true delete deploy httpd-deploy -n ${params.ENVIRONMENT}"
                }
            }
        }
        stage('Deploy httpd') {
        steps {
            withCredentials([
                string(credentialsId: 'minikube', variable: 'api_token')
                ]) {
                    //sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true apply -f httpd.yaml"
                    sh "kubectl --token $api_token --insecure-skip-tls-verify=true apply -f httpd.yaml -n ${params.ENVIRONMENT}"
                }
            }
        }
    }
}