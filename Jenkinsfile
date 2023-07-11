pipeline {
    agent any

    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "vkunal/aws-app"
        registryCredential = 'dockerhub'        
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script{
                    sh "sudo docker build -t ${registry}:${env.BUILD_ID}"

                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script{
                    sh "sudo docker run -dp 3000:3000 ${registry}:${env.BUILD_ID}"

                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script{
                    docker.withRegistry( 'https://hub.docker.com/', registryCredential ) {
                        sh "docker push ${registry}:${env.BUILD_ID}"
                    }

                }
            }
        }
    }
}
