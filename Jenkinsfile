properties([pipelineTriggers([githubPush()])])
pipeline {
    agent any

    stages {
        stage('Unit Tests') {
            steps {
                    echo 'Unit Tests Stage....'
		    git credentialsId: 'github-credential', url: 'https://github.com/clsowjanya/java-project.git'
				sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
            }
        }
        stage('Build') {
            steps {
		    echo 'Build stage....'
                sh 'ant -f build.xml -v'
            }
        }
 
	stage('Report') {
		steps {
			echo 'Report stage....'
			withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
				sh(" aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins")		
			}
		}
        }
	
    }
}
