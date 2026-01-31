pipeline{
	agent any
	environment{
		DOCKERHUB_CREDENTIALS=credentials('dockerhubID')
		DOCKER_IMAGE='josh57/prac1'
	}
	stages{
	stage('Checkout')
	{
		steps{
			git(url:'https://github.com/joshua-mnz/Lab-ex',branch:'main')
		}
	}
	stage('Build Docker Image')
	{
		steps{
		script{

		docker_Image=docker.build("${DOCKER_IMAGE}:latest")
	}}
	}
	stage('Push Image')
	{
		steps{
		script{
		docker.withRegistry('https://registry.hub.docker.com','dockerhubID')
		{
			docker_Image.push()
		}
	}
	}}

	}
	post{
		success{
		echo "Success"
		}
		failure{
		echo "Failure"
		}
		always
		{
			echo "Cleaning Workspace ....."
			deleteDir()
		}

	}

}
