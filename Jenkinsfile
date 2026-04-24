pipeline {
    agent any 

    stages {
        stage('Hello Python') {
            steps {
                // Inline command to verify Python is working
                sh 'python3 -c "print(\'Hello World from Python!\')"'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // 'SonarQubeServer' must match the name in Jenkins Global Configuration
                withSonarQubeEnv('SonarQubeServer') {
                    script {
                        // Locate the scanner tool defined in Global Tool Configuration
                        def scannerHome = tool 'SonarScanner' 
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        
        stage("Quality Gate") {
            steps {
                // Fails the build if SonarQube analysis doesn't meet your project's standards
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
