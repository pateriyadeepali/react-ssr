pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add commands to build the project, like `npm install` for Node.js
            }
        }
        stage('Deploy to AWS') {
            steps {
                echo 'Deploying to AWS...'
                // Commands to deploy, e.g., using `aws s3` or EC2 deployment script
            }
        }
    }
}
