pipeline {
    agent any 

    stages {
        stage('Run App') {
            steps {
                // This runs your existing app.py file
                sh 'python3 app.py'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Ensure 'SonarQubeServer' is the name you saved in Jenkins System settings
                withSonarQubeEnv('SonarQubeServer') {
                    script {
                        // This uses the SonarScanner tool you defined in Jenkins Global Tool Configuration
                        def scannerHome = tool 'SonarScanner' 
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        
        stage("Quality Gate") {
            steps {
                // This waits for SonarQube to finish and tell Jenkins if the code passed or failed
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}

