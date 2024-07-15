pipeline {
  agent any
  stages {
    stage('git pull') {
      steps {
        // github.com/k8s-edu/Bkv2_sub_gitops.git will replace by sed command before RUN
        git url: 'github.com/k8s-edu/Bkv2_sub_gitops.git', branch: 'main'
      }
    }
    stage('k8s deploy'){
      steps {
        withKubeConfig([credentialsId: 'cp-k8s', serverUrl: 'https://192.168.1.10:6443']) {
          sh 'kubectl apply -f deployment.yaml'
        }
      }
    }
  }
}
