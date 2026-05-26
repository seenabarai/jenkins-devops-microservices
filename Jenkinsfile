pipeline {
	agent any

	tools {
        jdk 'MyJDK'
    }

	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'MyMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
        

	}
	stages{
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH -$PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "BUILD TAG - $env.BUILD_TAG"
				echo "JOB NAME - $env.JOB_NAME"
				echo "BUILD URL - $env.BUILD_URL"
			}	
			
	    }
		stage('compile') {
			steps{
				sh "mvn clean compile"
			}
		
	    } 
	    stage('Test') {
			steps{
				sh "mvn test"
			}
		
	    } 
	    stage('Integration Test') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
	    }

		stage('Package') {
			steps{
				sh "mvn package -DskipTests"
			}
	    }	

		stage('Build Docker Image') {
			steps{
				script {
					dockerImage = docker.build("seenabarai/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps{
				script {
					docker.withRegistry('', 'dockerhub')
					dockerImage.push();
					dockerImage.push('latest');
				}
			}
		}

    }
	post{
		always{
			echo "I am awesome, I run always"
		}
		success{
			echo " I run only when you are successful"
		}
		failure{
			echo " I run only when you are fail"
		}
	}
}
