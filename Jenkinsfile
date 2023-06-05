pipeline {
  agent {
    docker {
      args '''-u 0:0
-p 3001:3000'''
      image 'alpine'
    }

  }
  stages {
    stage('build') {
      steps {
        sh 'apt-get install npm'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Package') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input ' Finished using the web site? (Select "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}