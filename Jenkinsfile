pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'ssh://git@utl-appgce01.pme.gb.telrock.net:2022/telrock-spring/telrock-tas', branch: '5.35.18-SNAPSHOT', changelog: true, credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097', poll: true)
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
}