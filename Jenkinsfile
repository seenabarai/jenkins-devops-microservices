pipeline {
	agent any

	tools {
        jdk 'MyJDK'
        maven 'MyMaven'
    }

	environment {
		dockerHome = tool 'MyDocker'
		PATH = "$dockerHome/bin:$PATH"
        

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
