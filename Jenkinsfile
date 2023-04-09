pipeline {
    agent any
    environment {
       email_list = 'shivam.singh@gslab.com'
       REPO_URL = 'https://github.com/shivamsingh3238/Clone-k8-s-poc.git'
       BRANCH_NAME = 'main'
       FOLDER_NAME = 'clone-poc'
       NEW_FOLDER_NAME = 'mynewfolder'
    }
    stages {
        stage('github checkout automatation-poc-repo') {
            steps {
                git 'https://github.com/shivamsingh3238/K8-s-POCs.git'
            }
        }
    

        // stage('Code Quality Check via SonarQubes'){
        //     steps {
        //        script {
        //        def scannerHome = tool 'SonarScanner';
        //            withSonarQubeEnv("SonarScanner") {
              
        //            sh "${tool("SonarScanner")}/bin/sonar-scanner"
        //                }
        //            }
        //         }
        // }
        // stage("Quality Gate") {
        //     steps {
        //       timeout(time: 1, unit: 'HOURS') {
        //         waitForQualityGate abortPipeline: true
        //       }
        //     }
        // }
      stage('Clone target repository') {
      steps {
        sh 'git clone --branch ${BRANCH_NAME} ${REPO_URL} temp_repo'
      }
    }
    
    stage('Copy workspace contents to temporary directory') {
      steps {
        sh "rsync -av --exclude='.git' . temp_repo"
      }
    }
    
    stage('Add and commit changes') {
      steps {
        dir('temp_repo') {
          sh 'git add .'
          sh 'git commit -m "Jenkins to GitHub"'
          sh "git  push origin ${BRANCH_NAME}"

        }
      }
    }     

  }
}