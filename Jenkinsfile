pipeline {
    agent any
    environment {
        registry = 'docker.io'
        registryCredential = '9f444712-3057-4261-bb69-0074b44794c6'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Abhinav97739/day15_prototype.git', branch: 'main'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    sh 'sudo docker build -t imperialx45/java-app:${env.BUILD_ID} .'
                    sh 'sudo docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}'
                    sh 'sudo docker push imperialx45/java-app:${env.BUILD_ID}'
                }
            }
        }
        stage('Deploy Container') {
            steps {
                script {
                    sh 'sudo docker run --name day_fifteen -d imperialx45/java-app:${env.BUILD_ID}'
                }
            }
        }
    }
}
