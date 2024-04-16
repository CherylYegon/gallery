pipeline {
    agent any
    
    stages {
        stage('Milestone 2: Basic Pipeline') {
            steps {
                git url: 'https://github.com/CherylYegon/gallery' // Specify the repository URL
                
                // Install required dependencies
                sh 'npm install'
                
                // Make change to landing page for Milestone 2
                sh 'echo "<h1>MILESTONE 2</h1>" > landing_page.html'
                
                // Deploy to Render
                sh 'node server'
                
                // Push changes to Render
                sh 'render deploy -- --branch main'
            }
            post {
                success {
                    // Send Slack message on successful deployment
                    script {
                        slackSend(channel: '#Cheryl_IP1', color: 'good', message: "MILESTONE 2 deployment successful! Build ID: ${env.BUILD_ID}. View deployment: ${env.RENDER_URL}")
                    }
                }
            }
        }
        
        stage('Milestone 3: Tests') {
            steps {
                // Switch to test branch and merge with main
                sh 'git checkout test && git merge main'
                
                // Run tests
                sh 'npm test'
                
                // Update landing page for Milestone 3
                sh 'echo "<h1>MILESTONE 3</h1>" >> landing_page.html'
                
                // Deploy to Render
                sh 'node server'
                
                // Push changes to Render
                sh 'render deploy -- --branch main'
            }
            post {
                success {
                    // Send Slack message on successful deployment
                    script {
                        slackSend(channel: '#Cheryl_IP1', color: 'good', message: "MILESTONE 3 deployment successful! Build ID: ${env.BUILD_ID}. View deployment: ${env.RENDER_URL}")
                    }
                }
                failure {
                    // Send email notification on test failure
                    emailext body: "Tests failed on Jenkins. Please investigate.",
                             subject: "Test Failure - ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                             to: "cyegon2023@gmail.com"
                }
            }
        }
    }
}
