#!/usr/bin/env groovy

pipeline{
    agent any
    stages{
        stage('test') {
            steps{
                script {
                    echo "Testing the app..."
                }
            }
        }
        stage("build") {
            steps{
                script {
                    echo "Building the app..."
                }
            }
        }
        stage("deploy") {
            steps{
                script {
                    //def dockerCmd = 'docker run -d -p 80:3080 --name demo-app kiseloff/react-nodejs-example:1.0'
                    def dockerComposeCmd = "docker compose -f docker-compose.yaml up"
                    sshagent(['ec2-server-key']) {
                        sh "scp docker-compose.yaml ec2-user@52.59.192.1:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@52.59.192.1 ${dockerComposeCmd}"
                    }
                }
            }
        }
    }
}
