pipeline {
    agent any
    environment {
       email_list = 'shivam.singh@gslab.com '
   }
    stages {
        stage('github checkout automatation-poc-repo') {
            steps {
                git 'https://github.com/shivamsingh3238/K8-s-POCs.git'
            }
        }

        stage('Code Quality Check via SonarQubes'){
            steps {
               script {
               def scannerHome = tool 'SonarScanner';
                   withSonarQubeEnv("SonarScanner") {
              
                   sh "${tool("SonarScanner")}/bin/sonar-scanner"
                       }
                   }
                }
        }
        
}
}
