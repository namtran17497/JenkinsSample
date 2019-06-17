pipeline {
  agent any
  stages {
    stage ('Findbugs Report') {
	  	steps {
			findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
	  	}	
  	}
  	stage ('SonarQube analysis') {
      	steps {
			withSonarQubeEnv('sonarqube1') {
  				sh './gradlew --info sonarqube'
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
