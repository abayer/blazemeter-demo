pipeline {

  agent any

  stages {

    stage('Run App Container') {
      steps {
        sh 'make app'
      }
    }

    stage('Run Taurus Perf Tests') {
      steps {
        bzt 'bzt-configs/the-test.yml'
      }
    }

  }

  post {
    always {
      sh 'make clean'
    }
  }
}
