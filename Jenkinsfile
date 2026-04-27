pipeline {
    agent any

    tools {
        // Must match the name in Manage Jenkins -> Tools -> SonarQube Scanner
        'hudson.plugins.sonar.SonarRunnerInstallation' 'SonarScanner'
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
                    // 1. This captures the actual installation path of the tool.
                    // 'SonarScanner' must match the Name in Manage Jenkins > Tools
                    def scannerHome = tool 'SonarScanner'
                    
                    // 2. Wrap the execution in the environment configured for your server.
                    // 'SonarQubeServer' must match the name in Manage Jenkins > System
                    withSonarQubeEnv('SonarQubeServer') {
                        sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=NewProject \
                        -Dsonar.projectName=NewProject \
                        -Dsonar.sources=. \
                        -Dsonar.python.version=3"

                    }
                }
            }
        }

        stage("Quality Gate") {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
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
