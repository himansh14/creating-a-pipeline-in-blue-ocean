pipeline {
  agent {
    docker {
      image 'alpine'
      args '-p 3001:3000'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '/usr/bin/npm install '
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