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
					archiveArtifacts artifacts: '**/*.war'
				}
			}
		}

		stage('Staging Area Deployment'){
			steps{
				echo 'Deploying to staging area'
				buid job: 'staging_job'
			}
			
		}

		stage('Production Area Deployment'){
			steps {
				timeout (time: 5, unit:'DAYS'){
					input message: 'Approve production deployment job?'
				}
				build job: 'production_job'
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