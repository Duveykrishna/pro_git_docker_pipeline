pipeline {
	agent any
	stages {
		stage("SCM pushing") {
			steps {
				git branch: 'main', url: 'https://github.com/Duveykrishna/pro_git_docker_pipeline.git'
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
				sh 'sudo docker tag java-repo:$BUILD_TAG duveykrishna/pipeline-java:$BUILD_TAG'
				}
			}
		}
	}
}
