@Library("Shared") _
pipeline {
    agent { label 'agent1' }

    stages {
        stage('Hello') {
            steps {
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
               script{
                   clone("https://github.com/muhammadaliazhar/node-todo-cicd.git","master")
               }
            }
        }
        stage('Build') {
            steps {
                script{
                    docker_build("maliazhar","node-app","latest")
                }
            }
        }
        stage("Push To DockerHub"){
            steps{
                script{
                    docker_push("node-app","latest","maliazhar")
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
