pipeline {
    agent any
    
    stages {
        stage('Set up') {
            steps {
                sh 'sed -i "s/<USERNAME>/cherylyegon/g" _config.js'
                sh 'sed -i "s/<PASSWORD>/RYLche123*/g" _config.js'
            }
        }
        stage('Basic pipeline') {
            environment {
                NODEJS = 'NODEJS'
            }
            tools {
                nodejs "NODEJS"
            }
            steps {
                sh 'npm install'
                sh 'node server &'
                
                sh 'echo "<h1>MILESTONE 2</h1>" >> index.html'
            }
        }
        stage('Tests') {
            environment {
                NODEJS = 'NODEJS'
            }
            tools {
                nodejs "NODEJS"
            }
            steps {
                sh 'git checkout -- test'
                
                sh 'npm install'
                
                sh 'git checkout master'
                sh 'git merge origin/test'
            }
        }
        stage('Call Render Webhook') {
            steps {
                script {
                    def webhookUrl = 'https://api.render.com/deploy/srv-cods5o8l6cac73bpjau0?key=0QQuMEDDNd8'
                    def response = sh(script: "curl -X POST ${webhookUrl}", returnStdout: true).trim()
                    echo "Webhook response: ${response}"
                }
            }
        stage('Slack integration') {
            steps {
                sh 'echo "<h1>MILESTONE 4</h1>" >> index.html'
            }
        }
    }
}
