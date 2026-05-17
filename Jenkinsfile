pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }

    stage('SonarCloud Analysis') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          sh '''
            rm -rf sonar-scanner sonar.zip sonar-scanner-*-linux*

            curl -sSLo sonar.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.0.2.4839-linux-aarch64.zip

            unzip -o sonar.zip

            mv sonar-scanner-7.0.2.4839-linux-aarch64 sonar-scanner

            ./sonar-scanner/bin/sonar-scanner -Dsonar.token=$SONAR_TOKEN
          '''
        }
      }
    }
  }
}