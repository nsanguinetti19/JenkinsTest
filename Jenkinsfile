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
		stage('Validaciones') {
			parallel {
				stage('Comparar Navegaciones') {
					steps {
						echo '----- Comparo Navegaciones -----'
					}
				}
				stage('Test Unitario') {
					steps {
						echo '----- Testing.. -----'
					}
				}
				stage('Comparar API') {
					steps {
						echo '----- Comparo API -----'
					}
				}
			}
		}
        stage('Deploy') {
			environment {
				KBDir = credentials('MTKBDir')
				TADir = credentials('MTTADir')
				TMDir = credentials('MTTMDir')
				BatchDir = credentials('MTBatchDir')
			}
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
			parallel {
				stage('Deploy TA') {
					steps {
						build job: 'MT - Deploy', parameters: [text(name: 'DeployOrigen', value: "${KBDir}"), text(name: 'DeployDestino', value: "${TADir}")]
					}
				}
				stage('Deploy Beta') {
					steps {
						build job: 'MT - Deploy', parameters: [text(name: 'DeployOrigen', value: "${KBDir}"), text(name: 'DeployDestino', value: "${TMDir}")]
					}
				}
				stage('Deploy BetaBatch') {
					steps {
						build job: 'MT - Deploy', parameters: [text(name: 'DeployOrigen', value: "${KBDir}\bin"), text(name: 'DeployDestino', value: "${MTBatchDir}")]
					}
				}
			}
        }
		stage('Testeo Integracion') {
			steps {
				echo '----- Testeo automático -----'
			}
		}
    }
}