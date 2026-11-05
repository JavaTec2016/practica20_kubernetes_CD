pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        bash '''java -version
            mvn --version
            git --version'''
      }
    }

    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernetes-jenkis-server-account', variable: 'api_token')
                      ]) {
            bash 'kubectl --token $api_token --server https://127.0.0.1:50955 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml '
          }

        }
      }

    }
  }