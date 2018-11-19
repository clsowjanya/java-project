properties([pipelineTriggers([githubPush()])])
pipeline {
    

    stages {
        stage('Unit Tests') {
            steps {
                    echo 'Unit Tests Stage....'
		   
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
  	stage('Deploy') {
            steps {
        	    echo 'Deploy stage....'
		    archiveArtifacts artifacts: 'dist/rectangle-${BUILD_NUMBER}.jar'
		    sh(" aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://assignment-9/rectangle-${BUILD_NUMBER}.jar")	
				
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
