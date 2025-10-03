pipeline {
    agent any
    
    stages {
        stage('Install Apache') {
            steps {
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y apache2'
            }
        }
        
        stage('Check for 4xx and 5xx Errors') {
            
            steps {
                
                script {
                    def logOutput = sh(script: 'sudo grep -E "(40[0-9]|41[0-9]|42[0-9]|43[0-9]|44[0-9]|45[0-9]|49[0-9]|50[0-9]|51[0-9]|52[0-9]|53[0-9])" /var/log/apache2/access.log || true', returnStdout: true)

                    if (logOutput) {
                        echo "HTTP errors were detected: \n${logOutput}"
                    } else {
                        echo "No 4xx or 5xx errors were detected."
                    }
                }
                
            }
            
        }
        
    }
    
}
