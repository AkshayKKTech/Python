pipeline {
    agent any

    tools {
        // Must match the name in Manage Jenkins -> Tools -> SonarQube Scanner
        sonarScanner 'SonarScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your git repository
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                    // Executes the static code scanning process
                    sh 'sonar-scanner'

                    }
                }
            }
        }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
