properties([pipelineTriggers([githubPush()])])
pipeline {
    agent any

    stages {
        stage('Unit Tests') {
            steps {
                git credentialsId: 'github-credential', url: 'https://github.com/clsowjanya/java-project.git'
				sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
            }
        }
        stage('Build') {
            steps {
                sh 'ant -f build.xml -v'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
