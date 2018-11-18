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
		    cp(file:'dist/rectangle-${BUILD_NUMBER}.jar', bucket:'assignment-9', path:'https://s3.console.aws.amazon.com/s3/buckets/assignment-9/?region=us-east-1&tab=overview/file.jar')
		
            }
        }
    }
}
