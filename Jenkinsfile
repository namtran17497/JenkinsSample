pipeline {
  agent any
  stages {
    stage ('Upload To Fabric') {
	    steps {
	    	sh 'bash ./gradlew clean build assembleDebug crashlyticsUploadDistributionDebug'
	    }	
    }
    stage ('Findbugs Report') {
	  	steps {
			findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
	  	}	
  	}
  	stage ('SonarQube analysis') {
      	steps {
			script {
  				// requires SonarQube Scanner 2.8+
  				scannerHome = tool 'SonarQube Scanner 2.8'
			}
			withSonarQubeEnv('SonarQube Scanner') {
  				sh './gradlew --info sonarqube'
			}
      	}
  	}
  }
}
