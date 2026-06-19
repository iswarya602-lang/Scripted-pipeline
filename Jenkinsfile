pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('docker-hub-login')
    }

    stages {

        stage('SCM') {
            steps {
                git 'https://github.com/iswarya602-lang/Scripted-pipeline.git'
            }
        }

        stage('Display Code') {
            steps {
                sh 'ls -lrt'
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

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t iswarya602-lang/myjenkins-pipeline:1.0 .'
            }
        }

        stage('Display Images') {
            steps {
                sh 'docker images'
            }
        }

        stage('Docker Login') {
            steps {
                sh '''
                echo $DOCKER_CREDENTIALS_PSW | docker login \
                -u $DOCKER_CREDENTIALS_USR --password-stdin
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push iswarya602-lang/myjenkins-pipeline:1.0'
            }
        }

    }
}
