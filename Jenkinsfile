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
        stage('List configmap'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'minikube', variable: 'api_token')]){
                        //getConfigMap="kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}"
                        //sh "kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}"
                        
                        configmap = sh (
                        script: "kubectl --token $api_token --insecure-skip-tls-verify=true get configmap/httpd-cm -o=name -n ${params.ENVIRONMENT}",returnStdout: true).trim()                       
                        echo "configmap: ${configmap}"
                        
                        if(configmap=="PASS")
                        {
                            echo 'test passed !!! '
                        
                       
                        }
                        

                        //if(!${configmap}.allWhitespace && !${configmap}.equals("No resources found.")){
                        //    configMapNames = configMap.split('\n')
                        //    for (int i=0; i <  configMapNames.length; i++){
                        //    command  = "kubectl delete configmap "+""+configMapNames[i].replace( 'configmap/', '' ).trim()+""+" -n "+${params.ENVIRONMENT}+" --grace-period=0 --force"                                    
                        //    println "configmap httpd-cm Listed"
                        //    }
                        //}
                        //else{
                        //println "No configmap httpd-cm Listed"
                        //}
                    }
                }
            }
        }
        //stage('Cleanup'){
        //    steps{
        //        echo "******Deployment To ******* ${params.ENVIRONMENT}"
        //        withCredentials([
        //        string(credentialsId: 'minikube', variable: 'api_token')
        //        ]) {
                    //sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true delete deploy httpd-deploy -n ${params.ENVIRONMENT}"
        //            sh "kubectl --token $api_token --insecure-skip-tls-verify=true delete deploy httpd-deploy -n ${params.ENVIRONMENT}"
        //        }
        //    }
        //}
        //stage('Deploy httpd') {
        //steps {
        //    withCredentials([
        //        string(credentialsId: 'minikube', variable: 'api_token')
        //        ]) {
                    //sh "kubectl --token $api_token --server https://192.168.99.100:8443 --insecure-skip-tls-verify=true apply -f httpd.yaml"
        //            sh "kubectl --token $api_token --insecure-skip-tls-verify=true apply -f httpd.yaml -n ${params.ENVIRONMENT}"
        //        }
        //    }
        //}
    }
}