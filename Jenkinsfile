pipeline {
  agent any
  stages {
//    stage ('Analysis') {
//	    steps{
//		    def mvnHome = tool 'mvn-default'
//	 
//	        sh "${mvnHome}/bin/mvn -batch-mode -V -U -e findbugs:findbugs"
//	         
//	        def findbugs = scanForIssues tool: [$class: 'FindBugs'], pattern: '**/target/findbugsXml.xml'
//	        publishIssues issues:[findbugs]
//	    }   
//	}
    stage ('Find bugs') {
	    steps {
		findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
	    }	
    }
    stage ('Upload To Fabric') {
	    steps {
		sh 'chmod +x gradlew'
	    	sh './gradlew clean findbugs build assembleDebug crashlyticsUploadDistributionDebug'
	    }	
    }
  }
}

//pipeline {
//    agent any
//    stages {
//        stage('Build') {
//            steps {
//                sh 'make' 
//                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
//            }
//        }
//        stage('Test') {
//            steps {
//                /* `make check` returns non-zero on test failures,
//                * using `true` to allow the Pipeline to continue nonetheless
//                */
//                sh 'make check || true' 
//                junit '**/target/*.xml'
//            }
//        }
//        stage('Deploy') {
//            when {
//              expression {
//                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
//              }
//            }
//            steps {
//                sh 'make publish'
//            }
//        }
//    }
//}
