pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
				bat "\"${tool 'MSBuild'}\" /t:Build /p:WorkingDirectory="C:\Continuous Integration\Sistemas\Metricas\KB\CIMT15" /p:ServerUsername="local\nsanguinetti" /p:ServerPassword="Brother.6180" /p:GX_PROGRAM_DIR="C:\Program Files (x86)\GeneXus\GeneXus15" /p:MSBuildExtensionsPath="C:\Program Files (x86)\MSBuild"
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
}