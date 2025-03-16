pipeline {
    agent any
     environment {
        DOCKER_CLI_PATH = '/usr/local/bin/docker'
    }
    tools {
        maven 'maven-3.9.9'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/bhawnachaudhary0805/Assignment2.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Cleanup') { 
            steps {
                sh '''#!/bin/bash
                CONTAINER_ID=$($DOCKER_CLI_PATH ps -q --filter ancestor=bhawnachaudhary/2022bcd0059)
                if [ ! -z "$CONTAINER_ID" ]; then
                    echo "Stopping and removing old container..."
                    $DOCKER_CLI_PATH stop $CONTAINER_ID
                    $DOCKER_CLI_PATH rm $CONTAINER_ID
                else
                    echo "No running container found."
                fi
                '''
            }
        }

         stage('Docker Build & Run') {
            steps {
                sh '$DOCKER_CLI_PATH build -t bhawnachaudhary/2022bcd0059 .'
                sh '$DOCKER_CLI_PATH run -d -p 9090:8080 bhawnachaudhary/2022bcd0059' 
            }
        }
    }
}
