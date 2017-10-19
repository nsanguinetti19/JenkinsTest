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
				/*build 'MT - Build'*/
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
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
			parallel {
				stage('Deploy Beta') {
					steps {
						echo '----- Comparo Navegaciones -----'
					}
				}
				stage('Deploy TA') {
					steps {
						echo '----- Testing.. -----'
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