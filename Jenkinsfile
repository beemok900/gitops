pipeline {
  agent any
  stages {
    stage('git pull') {
      steps {
        git url: 'https://github.com/beemok900/gitops.git', branch: 'main'
      }
    }
    stage('k8s deploy'){
      steps {
        withKubeConfig([credentialsId: 'k8s-auth', serverUrl: 'https://192.168.1.10:6443']) {
          sh 'kubectl apply -f deployment.yaml'
        }
      }
    }
  }
}
