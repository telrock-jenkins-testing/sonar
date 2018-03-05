pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo "Checking out ${env.gitUrl} ${env.buildBranch}"
        git(url: env.gitUrl, branch: env.buildBranch, credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097', poll: true, changelog: true)
      }
    }
    stage('Run') {
      steps {
        sh 'mvn sonar:sonar   -Dsonar.host.url=http://localhost:9000   -Dsonar.login=9e00f8b6dd1f8ff9fc16899749505766ba73cf8e'
      }
    }
    stage('wait') {
      steps {
        waitForQualityGate()
      }
    }
  }
  environment {
    gitUrl = 'https://coenie.basson@git.telrock-labs.com/telrock-spring/telrock-tas.git'
    buildBranch = '5.35.18-SNAPSHOT'
    jUnitPattern = '**/surefire-reports/*.xml'
    jBehaveReportDir = 'telrock-tas-karma/target/jbehave/view'
    jBehaveReportFiles = 'reports.html'
    jBehaveReportName = 'JBehave - Karma'
  }
}