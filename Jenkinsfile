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
	    	sh 'bash ./gradlew clean build assembleDebug'
	    	fabric apiKey: '35848c431606d9c235810ec6c8e7838bb3be9271', apkPath: 'app/build/outputs/apk/debug/app-debug.apk', buildSecret: 'df9d968bd9b9bfed2f5e99186d2d2be9aa22baa252b34c183e4ff80ffb631e95', notifyTestersType: 'NOTIFY_TESTERS_GROUP', organization: 'CICD', releaseNotesFile: 'release_notes.txt', releaseNotesParameter: 'FABRIC_RELEASE_NOTES', releaseNotesType: 'RELEASE_NOTES_FROM_CHANGELOG', testersEmails: '', testersGroup: 'QA', useAntStyleInclude: false
	    }	
    }
  }
}
