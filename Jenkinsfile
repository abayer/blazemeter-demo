pipeline {
  agent any
  stages {
    stage('Run App') {
      steps {
        sh 'make app'
      }
    }
    stage('Run Perf Tests') {
      steps {
        sh 'pwd && ls'
        sh 'mkdir artifacts'
        sh 'pwd && ls'
        sh 'make bzt'
        sh 'pwd && ls'
        sh 'cd artifacts && ls'
      }
    }
    stage('Publish Test Results') {
      steps {
        //see JENKINS-32650 and JENKINS-31967
        performanceReport compareBuildPrevious: false, configType: '', errorFailedThreshold: -1, errorUnstableResponseTimeThreshold: '', errorUnstableThreshold: -1, failBuildIfNoResultFile: false, modeOfThreshold: false, modePerformancePerTestCase: true, modeThroughput: false, nthBuildNumber: 0, relativeFailedThresholdNegative: -1, relativeFailedThresholdPositive: -1, relativeUnstableThresholdNegative: -1, relativeUnstableThresholdPositive: -1, sourceDataFiles: "$WORKSPACE/artifacts/result.xml"
      }
    }
  }
  post {
    always {
      sh 'make clean'
    }
  }
}
