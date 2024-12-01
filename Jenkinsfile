pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Pull the latest code from the repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Build the application using Gradle
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                // Run tests using Gradle
                sh './gradlew test'
            }
        }
    }
    post {
        always {
            // Archive test results and notify if necessary
            junit '**/build/test-results/test/*.xml'
            archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
        }
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed. Please check logs.'
        }
    }
}

