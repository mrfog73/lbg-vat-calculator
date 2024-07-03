pipeline {

  agent any

  stages {
    stage('Checkout') {
      steps {
        // Get some code from a GitHub repository
        git branch: 'main', url: 'https://github.com/mrfog73/lbg-vat-calculator.git'
      }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
      steps {
        withSonarQubeEnv('sonar-qube-1') {        
          sh "${scannerHome}/bin/sonar-scanner"
        }   
	      timeout(time: 110, unit: 'MINUTES'){
	        waitForQualityGate abortPipeline: true
	      }
      }
    }
  }
}
