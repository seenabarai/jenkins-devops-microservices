pipeline {
	agent any

	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'MyMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
        

	}
	stages{
		stage('Build') {
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
	    stage('Test') {
			steps{
				echo "Test"
			}
		
	    } 
	    stage('Integration Test') {
			steps{
				echo "Integration Test"
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
