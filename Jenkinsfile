pipeline{
    agent{
        label 'agent1'
    }

    stages{
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image'){
            steps{
                script{
                    sh """
                        docker build -t youssif37/petclinic .
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
                            docker push youssif37/petclinic
                        """
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    sh "docker-compose up -d"
                }
            }
        }

    }
}
