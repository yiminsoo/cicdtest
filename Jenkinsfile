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
        docker pull yiminsoo/cicdtest:gold
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deployment myweb-gold --image=yiminsoo/cicdtest:gold'
        ansible master -m command -a 'kubectl expose deployment myweb-gold --type=LoadBalancer --port=80 --name=myweb-gold'

        '''
      }
    }
  }
}
