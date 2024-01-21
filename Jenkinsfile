pipeline {
    agent any

    environment {
        WEATHER_API_KEY = '9d9bf5bb1db3418e9de201008242001'
    }

    stages {
        stage('Git Clone') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: 'main']],
                    userRemoteConfigs: [[url: 'https://github.com/boufi9/CC_G5.git']]])
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t microservicemeteo-eurekaserver ./eurekaserver'
                    bat 'docker build -t microservicemeteo-user-service ./user-service'
                    bat 'docker build -t microservicemeteo-notification-service ./notification-service'
                    bat 'docker build -t microservicemeteo-meteo-service ./meteo-service'
                    bat 'docker build -t microservicemeteo-gateway ./gateway'
                }
            }
        }


        stage('Run Docker Containers') {
            steps {
                script {
                    bat 'docker run -d --name eurekaserver -e WEATHER_API_KEY=${WEATHER_API_KEY} microservicemeteo-eurekaserver'
                    bat 'docker run -d --name user-service -e WEATHER_API_KEY=${WEATHER_API_KEY} microservicemeteo-user-service'
                    bat 'docker run -d --name notification-service -e WEATHER_API_KEY=${WEATHER_API_KEY} microservicemeteo-notification-service'
                    bat 'docker run -d --name meteo-service -e WEATHER_API_KEY=${WEATHER_API_KEY} microservicemeteo-meteo-service'
                    bat 'docker run -d --name gateway -e WEATHER_API_KEY=${WEATHER_API_KEY} microservicemeteo-gateway'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            bat 'docker stop eurekaserver user-service notification-service meteo-service gateway'
            bat 'docker rm eurekaserver user-service notification-service meteo-service gateway'
        }
    }
}
