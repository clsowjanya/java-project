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
 	    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAJDZYCW5FP2DPR5VA', credentialsId: '', secretKeyVariable: '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']]) {
		sh(" aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins")		
	    }
          }
        }
	
    }
}
