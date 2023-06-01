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
			stage("Docker Hub") {
			steps {
			withCredentials([string(credentialsId: 'docker_hub_passwd', variable: 'docker_hub_password_var')]) {
				sh 'sudo docker login -u soft14308 -p ${docker_hub_password_var}'
				sh 'sudo docker push soft14308/gitbash:$BUILD_TAG'
				}
			}

		}
		stage("QAT Testing") {
			steps {
				sh 'sudo docker rm -f $(sudo docker ps -a -q)'
				sh 'sudo docker run -dit -p 8080:8080 soft14308/gitbash:$BUILD_TAG'
				}
			}
		}
}
}

