pipeline {
    agent any

    tools {
        // Must match the name in Manage Jenkins -> Tools -> SonarQube Scanner
        "sonar-scanner" 'SonarScanner'
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
                        def scannerHome = tool 'SonarScanner'
                        sh "${scannerHome}/bin/sonar-scanner"

                    }
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
