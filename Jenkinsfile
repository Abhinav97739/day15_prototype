pipeline {
    agent any
    environment {
        registry = 'docker.io'  
        registryCredential = '482c000e-ef9b-4e20-b628-1236f0eaae4b' 
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Abhinav97739/day15_prototype.git', branch: 'main'
            }
        }
        stage('build image') {
            steps{
                script{
                    docker.withRegistry('', registryCredential){
                        def customImage = docker.build("imperialx45/java-app:${env.BUILD_ID}")
                        customImage.push()

                    }
                }
            }
        }
        stage('Deploy Container') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        def runContainer = docker.image("imperialx45/java-app:${env.BUILD_ID}").run('--name day_fifteen -d')
                        echo "Container ID: ${runContainer.id}"
                    }
                }
            }
        }
    }
}
 
