pipeline {
    agent any
    environment {
        registry = 'docker.io'  
        registryCredential = 'e525fa9e-cefd-42de-b160-9e806a87faa1' 
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
 
