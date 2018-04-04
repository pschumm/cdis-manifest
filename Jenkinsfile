#!groovy

pipeline {
  agent any

  stages {
    stage('FetchCode') {
      steps {
        checkout scm
         git(
            url: 'https://github.com/uc-cdis/cloud-automation.git',
            branch: 'chore/jenkins-qa'
          )
      }
    }
    stage('k8sDeploy') {
        steps {
            echo "GIT_BRANCH is $env.GIT_BRANCH"
            echo "GIT_COMMIT is $env.GIT_COMMIT"
            echo "WORKSPACE is $env.WORKSPACE"
            sh "find ."
        }
    }
  }
  post {
    success {
      echo "https://jenkins.planx-pla.net/ $env.JOB_NAME pipeline succeeded"
    }
    failure {
      slackSend color: 'bad', message: "https://jenkins.planx-pla.net $env.JOB_NAME pipeline failed"
    }
    unstable {
      slackSend color: 'bad', message: "https://jenkins.planx-pla.net $env.JOB_NAME pipeline unstable"
    }
  }
}
