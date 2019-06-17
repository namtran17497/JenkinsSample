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
			withSonarQubeEnv('SonarQube Scanner') {
  				sh './gradlew --info sonarqube'
			}
      	}
  	}
  }
}
