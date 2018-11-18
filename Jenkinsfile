properties([pipelineTriggers([githubPush()])])

node('linux') { 
	
		stage('Unit Tests') {    
			steps {
				git credentialsId: 'github-credential', url: 'https://github.com/clsowjanya/java-project.git'
				sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
			}
		}
		
	
}
