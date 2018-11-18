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
		  writeFile file: "output/rectangle-${BUILD_NUMBER}.jar", text: "This file is useful, need to archive it."

		
		
            }
        }
    }
}
