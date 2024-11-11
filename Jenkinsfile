pipeline {
    agent any
    environment {
        // Set environment variables for AWS credentials (replace with actual keys in a secure way)
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        S3_BUCKET_NAME = 'my-react-ssr-bucket'
        EC2_INSTANCE_IP =  3.108.16.66
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing project dependencies...'
                sh 'npm install'  // Install Node.js dependencies
            }
        }
        
        stage('Build Project') {
            steps {
                echo 'Building the React SSR project...'
                sh 'npm run build'  // Run the build command to generate production files
            }
        }

        stage('Deploy to AWS S3') {
            steps {
                echo 'Deploying project to AWS S3...'
                sh 'aws s3 sync ./build s3://$S3_BUCKET_NAME --delete'  // Sync build files to S3
            }
        }
        
        stage('Deploy to AWS EC2') {
            steps {
                echo 'Deploying project to AWS EC2...'
                // Connect to EC2 and deploy project files
                sh '''
                    ssh -o StrictHostKeyChecking=no ec2-user@$EC2_INSTANCE_IP << EOF
                    # Navigate to your project directory and update files
                    cd /path/to/project/on/ec2
                    git pull origin master
                    npm install
                    npm run start
                    EOF
                '''
            }
        }
    }
}
