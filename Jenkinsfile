pipeline {
    agent any

    stages {
        stage('Update') {
            steps {
                echo '----- Update from GXServer -----'
				build 'MT - Update'
            }
        }
		stage('Build') {
		    when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo '----- Building MT -----'
				build 'MT - Build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo 'Deploying'
            }
        }
    }
	post {
        success {
            mail to: nsanguinetti@concepto.com.uy, subject: 'The Pipeline success :)'
        }
        unstable {
            mail to: nsanguinetti@concepto.com.uy, subject: 'The Pipeline is unstable :|'
        }
		failure {
            mail to: nsanguinetti@concepto.com.uy, subject: 'The Pipeline failed :('
        }
    }
}