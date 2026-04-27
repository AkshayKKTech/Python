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
                // 'SonarQube' must match the name in Manage Jenkins -> System -> SonarQube Server
                withSonarQubeEnv('SonarQubeServer') {
                    sh """
                        sonar-scanner \
                        -Dsonar.projectKey=NewProject \
                        -Dsonar.projectName="NewProject" \
                        -Dsonar.branch.name=master \
                        -Dsonar.sources=. \
                        -Dsonar.language=py \
                        -Dsonar.python.version=3
                    """
                }
            }
        }

        stage("Quality Gate") {
            steps {
                // This pauses the pipeline until SonarQube finishes the background task.
                // Note: Requires a Webhook configured in SonarQube pointing to Jenkins.
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
        success {
            echo 'Code analysis passed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the SonarQube Quality Gate or Logs.'
        }
    }
}


