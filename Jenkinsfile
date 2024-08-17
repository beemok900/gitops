pipeline {
  agent any
  stages {
    stage('deploy start') {
      steps {
        slackSend(message: "Deploy ${env.BUILD_NUMBER} Started"
        , color: 'good', tokenCredentialId: 'slack-key')
      }
    }      

    stage('git pull') {
      steps {
        // https://github.com/beemok900/gitops.git will replace by sed command before RUN
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

    stage('deploy end') {
      steps {
        slackSend(message: """${env.JOB_NAME} #${env.BUILD_NUMBER} End
        """, color: 'good', tokenCredentialId: 'slack-key')
      }
    }
  }
}
