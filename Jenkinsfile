pipeline {
    environment {
    imagename = "pratiksb/python-static:v3"
    registryCredential = 'test-demo-docker'
    dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/Pratikbhusanur/pratik-docker-jenkin-python-demo.git', branch: 'main'])
             }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build imagename 
                }
            }
        }
        stage('Deploy Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("V3 + $BUILD_NUMBER")
                    //dockerImage.push('latest')
                     }
                 }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $imagename:$BUILD_NUMBER"
                sh "docker rmi $imagename:latest"
            }
        }
    }
}


