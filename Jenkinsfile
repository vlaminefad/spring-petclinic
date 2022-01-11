pipeline {
    agent any
    stages {
        stage('Initialize'){
            steps {
                script {
                    def dockerHome = tool 'docker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                    service docker start
                }
            }
        }
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build "safiaeb/petclinic:$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    // Assume the Docker Hub registry by passing an empty string as the first parameter
                    docker.withRegistry('' , 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
