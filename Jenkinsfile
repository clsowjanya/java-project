properties([pipelineTriggers([githubPush()])])

node('linux') { 
	agent any
	stage('Unit Tests') {    
		git credentialsId: 'github-credential', url: 'https://github.com/clsowjanya/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Results') {    
		junit 'reports/*.xml'   
	}
}
