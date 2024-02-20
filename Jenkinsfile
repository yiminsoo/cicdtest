pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/yiminsoo/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t 211.183.3.100:8443/echo-ip .
        docker push 211.183.3.100:8443/echo-ip
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment pl-bulk-prod --image=211.183.3.100:8443/echo-ip
        kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 --name=pl-bulk-prod-

        '''
      }
    }
  }
}
