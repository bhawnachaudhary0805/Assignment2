pipeline {
    agent any

    environment {
        IMAGE_NAME = "bhawnachaudhary/2022BCD0059"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/bhawnachaudhary0805/Assignment2'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build & Run') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
                sh "docker run -d -p 9090:8080 ${IMAGE_NAME}"
            }
        }
    }
}
