pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo "Checking out ${env.gitUrl} ${env.buildBranch}"
        git(url: env.gitUrl, branch: env.buildBranch, credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097', poll: true, changelog: true)
      }
    }
    stage('SonarQube analysis') {
		steps {
		    withSonarQubeEnv('SonarQube') {
		      // requires SonarQube Scanner for Maven 3.2+
		      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
		    }
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
    buildBranch = 'rc/5.35.18-SNAPSHOT'
    jUnitPattern = '**/surefire-reports/*.xml'
    jBehaveReportDir = 'telrock-tas-karma/target/jbehave/view'
    jBehaveReportFiles = 'reports.html'
    jBehaveReportName = 'JBehave - Karma'
  }
}
