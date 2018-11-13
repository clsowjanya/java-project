properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git credentialsId: 'github-credential', url: 'https://github.com/clsowjanya/java-project.git'
		sh 'ant -buildfile test.xml'   
	}   
	stage('Build') {    
		sh 'ant'   
	}   
	stage('Results') {    
		junit 'reports/*.xml'   
	}
}
