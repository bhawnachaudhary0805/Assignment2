pipeline {
    agent any
     environment {
        DOCKER_CLI_PATH = '/usr/local/bin/docker'
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_PROJECT_KEY = 'java-service'
        SONAR_LOGIN_TOKEN = credentials('jenkins-sonar-token')
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
        stage('SonarQube Analysis') {
            steps {
                sh '''
                mvn sonar:sonar \
                    -Dsonar.projectKey=$SONAR_PROJECT_KEY \
                    -Dsonar.host.url=$SONAR_HOST_URL \
                    -Dsonar.login=$SONAR_LOGIN_TOKEN
                '''
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
