pipeline {
  agent any
  stages {
    stage('Run App Container') {
      steps {
        sh '''make app
echo "Hi there, I'm going to run a build. Hopefully."'''
      }
    }
    stage('Run Taurus Perf Tests') {
      steps {
        bzt 'bzt-configs/the-test.yml'
      }
    }
    stage('Deploy') {
      when {
        expression {
          currentBuild.result != "UNSTABLE"
        }
        
      }
      steps {
        echo 'Deploying...'
        mail(subject: 'Hey, I deployed something. You may regret giving me this power.', body: 'Bwahahahahahahahahahaha*choke*', to: 'abayer@cloudbees.com')
      }
    }
  }
  post {
    always {
      sh 'make clean'
      
    }
    
    unstable {
      echo 'Unstable!'
      
    }
    
  }
}