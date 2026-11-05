pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        shell '''java -version
            mvn --version
            git --version'''
      }
    }

    stage('Deploy billing App') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'kubernetes-jenkis-server-account',
                        variable: 'api_token'
                    )
                ]) {
                    shell '''
                        @echo off
                        echo Verificando conexion con Kubernetes...

                        kubectl --token "%api_token%" --server https://127.0.0.1:55955 --insecure-skip-tls-verify=true get nodes

                        echo Aplicando manifiesto de Kubernetes...

                        kubectl --token "%api_token%" --server https://127.0.0.1:55955 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml

                        echo Verificando deployments...
                        kubectl --token "%api_token%" --server https://127.0.0.1:55955 --insecure-skip-tls-verify=true get deployments
                    '''
                }
            }
        }
    }
}