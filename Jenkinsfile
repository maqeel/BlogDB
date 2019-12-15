pipeline {
	agent any
	environment {
		registryCredential = 'dockerhub'
		}

	stages {
		stage('Build') {
			steps {
				sh 'docker build -t aqeel4mpak/blog_db .'
			}
		}
		stage('Test') {
			steps {
				sh 'docker container rm -f blogDB || true'
				sh 'docker container run -p 5432:5432 --name blogDB -d aqeel4mpak/blog_db'
				sh 'sleep 30'
			}
		}
		stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
					sh 'docker push aqeel4mpak/blog_db:latest'
					}
				}
			}
		}
	}
}
