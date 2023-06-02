pipeline{
	
	agent {
		label "ubuntu"
		}
		stages{
			stage ("Pull the code from SCM"){
				steps {
					git branch: 'main', url: 'https://github.com/gouravaas/new_java_docker_app.git'
					}
				}
			stage (" Build the code "){
				steps {
					sh 'sudo mvn dependency:purge-local-repository'
					sh 'sudo mvn clean package'
					}
				}
			stage (" Build the image "){
				steps {
					sh 'sudo docker build -t java-repo:$BUILD_TAG .'
					sh 'sudo docker tag java-repo:$BUILD_TAG soft14308/java-app:$BUILD_TAG'
					}
				}
                        stage ( " push the image "){
				steps {
					withCredentials([string(credentialsId: 'docker_hub_passwd', variable: 'docker_hub_password_var')]){
					sh 'sudo docker login -u soft14308 -p $docker_hub_password_var'
					sh 'sudo docker push soft14308/java-app:$BUILD_TAG'
						}
					}
				}
			stage("QAT Testing") {
				steps {
					script {
						sh 'sudo docker run -dit -p 8080:8080 soft14308/java-app:$BUILD_TAG'
						}
					}
				}
			stage("testing website") {
				steps {
					retry(5) {
						script {
							sh 'curl --silent http://43.205.124.201:8080/java-web-app/ | grep -i "india" > /home/ubuntu/test.txt'

							}
						}
					}
				}
		}
}
