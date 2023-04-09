pipeline {
    agent any
    environment {
       email_list = 'shivam.singh@gslab.com'
       REPO_URL = 'https://github.com/shivamsingh3238/Clone-k8-s-poc.git'
       BRANCH_NAME = 'master'
       FOLDER_NAME = 'clone-poc'
       NEW_FOLDER_NAME = 'mynewfolder'
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
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        }
        stage('Clone or pull repository') {
            steps {
                script {
                    sh "cd .."
                    if (fileExists(FOLDER_NAME)) {
                        echo "Folder already exists. Skipping creation."
                        sh "git -C ${FOLDER_NAME} pull origin ${BRANCH_NAME}"
                        sh "ls"
                        sh "pwd"
                    } else {
                        echo "Folder does not exist. Creating."
                        sh "mkdir ${FOLDER_NAME}"
                        sh "git clone --branch ${BRANCH_NAME} ${REPO_URL} ${FOLDER_NAME}"
                        sh "ls"
                        sh "pwd"
                    }
                    
                    sh "mkdir ${NEW_FOLDER_NAME}"
                    sh "ls -ltr"
                    
                }
            }
        }
    }
}
