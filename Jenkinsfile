pipeline {
    agent { label "agent1" }

    stages {
        stage('Code') {
            steps {
                git url: "https://github.com/muhammadaliazhar/node-todo-cicd.git", branch: "master"
            }
        }
        stage('Build') {
            steps {
                sh "docker build -t node-app1:latest ."
            }
        }
        stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh 'docker login -u $dockerHubUser -p $dockerHubPass'
                sh "docker image tag node-app1:latest ${env.dockerHubUser}/node-app1:latest"
                sh "docker push ${env.dockerHubUser}/node-app1:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}
