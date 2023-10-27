pipeline {
    agent any  // This runs the pipeline on any available agent (node/agent)

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                script {
                    git 'https://github.com/akashgaikwad0209/akash.git'
                }
            }
        }

        stage('Build') {
            steps {
                // Build your application (replace this with your build commands)
                sh 'echo "Testing"'
            }
        }

        stage('Test') {
            steps {
                // Run tests (replace this with your test commands)
                sh 'echo "Testing"'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy your application (replace this with your deployment commands)
                sh 'echo "Testing"'
            }
        }
    }

    post {
        success {
            // This block of code will be executed if the pipeline runs successfully
            echo 'Pipeline succeeded! Deploying to production...'
            // Add deployment to production steps here
        }
        failure {
            // This block of code will be executed if the pipeline fails
            echo 'Pipeline failed! Not deploying to production.'
        }
    }
}
