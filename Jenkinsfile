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
                        
                    println "configmap" configmap

                        //GIT_COMMIT_EMAIL = sh (
                        //    script: 'git --no-pager show -s --format=\'%ae\'',returnStdout: true).trim()
                        //    echo "Git committer email: ${GIT_COMMIT_EMAIL}"
                        //if(!configMap.allWhitespace && !configMap.equals("No resources found.")){
                        //    def configMapNames = configMap.split('\n')
                        //    for (int i=0; i <  configMapNames.length; i++){
                        //    def command  = "kubectl delete configmap "+""+configMapNames[i].replace( 'configmap/', '' ).trim()+""+" -n "+${params.ENVIRONMENT}+" --grace-period=0 --force"        
                            
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