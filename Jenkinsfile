pipeline {
    agent {
        label 'Agent1'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your git repository
                checkout scm
            }
        }

      /*  stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    
                    // Executes the scanning environment wrapper using the server configuration name
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"

                    }
                }
            }*/
        stage('Build') {
            steps {
                echo " Building the app"
                sh "python3 app.py"
    }
}

    post {
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
