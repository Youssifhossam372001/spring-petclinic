pipeline{
    agent{
        label 'agent1'
    }

    stages{
        stage('Build Docker Image'){
            steps{
                script{
                    def repoUrl = 'https://github.com/Youssifhossam372001/spring-petclinic'
                    sh """
                        git clone ${repoUrl} app

                        cd app
                        docker build -t petclinic .
                    """
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    def dockerHubCredentialsId = 'dockerhub'
                    withDockerRegistry([credentialsId: "${dockerHubCredentialsId}", url: ""]) {
                        sh """
                            docker push petclinic
                        """
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    def dockerComposePath = 'app/docker-compose.yaml' 
                    sh "docker-compose -f ${dockerComposePath} up -d"
                }
            }
        }

    }
}
