pipeline {
    agent any

    tools {
        maven 'New maven'
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
                sh '''
                docker build -t iswaryasundaramoorthy/git-version-control:1.0 .
                '''
            }
        }

        stage('Display Images') {
            steps {
                sh 'docker images'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker-hub-login',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                docker push iswaryasundaramoorthy/git-version-control:1.0
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Docker image built and pushed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
