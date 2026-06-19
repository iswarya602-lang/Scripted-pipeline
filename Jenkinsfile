pipeline {
agent any
environment {
DOCKER_CREDENTIALS = creden􀆟als('docker-hub-login')
}
stages {
stage('SCM') {
steps {
git branch: 'main', changelog: false, poll: false, url:
'https://github.com/techfarmersrikanth/sample-java-app.git'
}
}
stage("Display the code") {
steps {
sh 'ls -lrt'
}
}
stage("Build") {
steps {
sh 'mvn package'
}
}
stage("Test") {
steps {
sh 'mvn test'
}
}
stage("docker-image") {
steps {
sh 'docker build -t srikanthdev1/myjenkins-pipeline:1.0 .'
}
}
stage("display-image") {
steps {
sh 'docker images'
}
}
stage("docker-login") {
steps {
sh "echo $DOCKER_CREDENTIALS_PSW | docker login -u
$DOCKER_CREDENTIALS_USR --password-stdin"
}
}
stage("docker-push") {
steps {
sh "docker push srikanthdev1/myjenkins-pipeline:1.0"
}
}
}
}
