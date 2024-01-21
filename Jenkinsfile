pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build and Push') {
            steps {
                script {
                    dockerImage = docker.build("my-image:${env.BUILD_ID}")
                    // If you need to push the image to a registry, uncomment the next line
                    // dockerImage.push()
                }
            }
        }
    }
    post {
        always {
        }
    }
}
