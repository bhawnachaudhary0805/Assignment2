pipeline {
    agent any

    environment {
        IMAGE_NAME = "bhawnachaudhary/2022BCD0059"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 
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
                sh "docker run -d -p 8080:8080 ${IMAGE_NAME}"
            }
        }
    }
}
