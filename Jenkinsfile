pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "k8s-minikube-dev-production"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
