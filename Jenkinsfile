pipeline{
    agent{
        label 'agent1'
    }

    stages{
        stage('Maven Install') {
            agent {         
                docker {          
                    image 'maven:3.5.0'         
                }       
            }       
            steps {
                sh 'mvn clean install'
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
