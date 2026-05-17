pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js project dependencies using npm.'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running project test cases.'
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating test coverage report.'
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit Security Scan') {
            steps {
                echo 'Running npm audit to identify known dependency vulnerabilities and CVEs.'
                sh 'npm audit || true'
            }
        }
    }

    post {
        always {
            echo 'DevSecOps basic pipeline completed. Review console output for npm audit findings.'
        }

        success {
            echo 'Pipeline finished successfully.'
        }

        failure {
            echo 'Pipeline failed, but security findings may still be visible in console output.'
        }
    }
}
