pipeline {
    agent test  // This runs the pipeline on any available agent (node/agent)

    stages {
        stage('Build') {
            steps {
                // Build your application (replace this with your build commands)
                bat 'echo "Testing"'
            }
        }

    stage('Runiing test stage parallel') {

        parallel {
        stage('Test1') {
            steps {
                // Run tests (replace this with your test commands)
                println env.GIT_BRANCH
                bat 'echo "env.GIT_BRANCH"'
                sleep 60
            }
        }

                stage('Test') {
            steps {
                // Run tests (replace this with your test commands)
                println env.GIT_BRANCH
                bat 'echo "env.GIT_BRANCH"'
                sleep 60
            }
        }
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
