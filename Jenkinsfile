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
  		iDir = 'cov-idir'
  		steps {
  			withCoverityEnv(coverityToolName: 'default', hostVariable: '', passwordVariable: '', portVariable: '', usernameVariable: '') {
    			// run cov-build capture command
			    sh "cov-build --dir ${iDir} <build-command>"
			  
			    // run cov-analyze command
			    sh "cov-analyze --dir ${iDir}"

			    // run cov-commit-defects command
			    sh "cov-commit-defects --dir ${iDir} --host ${COVERITY_HOST} --port ${COVERITY_PORT} --stream my stream"
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
