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
  	stage ('Coverity Analysis')	{
  		steps {
  			withCoverityEnv(coverityToolName: 'default', hostVariable: '', passwordVariable: '', portVariable: '', usernameVariable: '') {
    			// run cov-build capture command
			    sh "cov-build --dir cov-idir <build command>"
			  
			    // run cov-analyze command
			    sh "cov-analyze --dir cov-idir"
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
