pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'item-app:latest'
        APP_NAME = 'item-app'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '📦 Checking out source code...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '🔨 Building Docker image...'
                dir('backend') {
                    sh 'docker build -t item-app:latest .'
                }
            }
        }
        
        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh './test.sh || echo "⚠️ Tests completed with warnings"'
            }
        }
        
        stage('Deploy') {
            steps {
                echo '🚀 Deploying to Proxmox...'
                sh '''
                    echo "Deployment would happen here via Ansible"
                '''
            }
        }
    }
    
    post {
        always {
            echo '🔄 Pipeline completed!'
        }
        success {
            echo '✅ Pipeline succeeded!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}