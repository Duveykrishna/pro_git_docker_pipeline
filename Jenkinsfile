pipeline {
	agent any
	stages {
		stage("SCM pushing") {
			steps {
				git 'https://github.com/gouravaas/java_docker_app.git'
				}
			}

		stage("build") {
			steps {
				sh 'sudo mvn dependency:purge-local-repository'
				sh 'sudo mvn clean package'
				}
			}
		stage("Image") {
			steps {
				sh 'sudo docker build -t java-repo:$BUILD_TAG .'
				sh 'sudo docker tag java-repo:$BUILD_TAG Gouravaas/pipeline-java:$BUILD_TAG'
				}
			}
		}
	}
}
