pipeline {
  agent any
  stages {
    stage ('Findbugs Report') {
	  	steps {
			findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
	  	}	
  	}
  	stage ('SonarQube Analysis') {
      	environment {
        	scannerHome = tool 'sonarqubeScanner'
	    }
	    steps {
	        withSonarQubeEnv('sonarqube1') {
	            sh "${scannerHome}/bin/sonar-scanner"
	        }
	    }
  	}
    stage ('Upload To Fabric') {
	    steps {
	    	sh 'bash ./gradlew clean build assembleDebug crashlyticsUploadDistributionDebug'
	    }	
    }
  }
}
