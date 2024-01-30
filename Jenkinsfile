pipeline {
    environment{
        registry = "yannsko78/helloword"
        registryCredential = 'dockerhub'
        dockerImage= ' '
    }

    agent any
    
    stages{
        stage('Git checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Building image') {
            steps{
                dir('app'){
                    script{
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential) {
                        dockerImage.push()
                        dockerImage.push("latest")
                    }
                    echo " trying to push docker build to dockerhub "
                }
            }
        }
        stage ("Remove Unused docker image"){
            steps{
                bat " docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}