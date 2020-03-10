pipeline {
	agent any
	stages{
		stage('Package and Build Stage'){
			steps {
				bat 'mvn clean package'
			}
			post{
				success{
					echo 'job successfully packaged and build'
					archiveArtifacts artifacts : '**/*.war'
				}
			}
		}
		stage('Staging Area Deployment'){
			steps{
				echo 'Deploying to staging area'
				build job: 'KimWeb_Stagging_Pipeline'
			}
			
		}
		stage('Production Area Deployment'){
			steps {
				timeout (time: 5, unit:'DAYS'){
					input message: 'Approve production deployment job?'
				}
				build job: 'KimWeb_Production_Pipeline'
			}
			post {
				success{
					echo 'Production deployment successful'
				}
				failure{
					echo 'Production deployment failed'
				}
			}

		}
	}
}