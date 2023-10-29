pipeline {
    agent any

    parameters {
        booleanParam(name: 'BUILD', defaultValue: true, description: 'Build the application')
        booleanParam(name: 'UPLOAD_ARTIFACT', defaultValue: true, description: 'Upload the artifact')
    }

    stages {
        stage('Build') {
            when {
                expression { params.BUILD }
            }
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Artifact Upload') {
            when {
                expression { params.UPLOAD_ARTIFACT }
            }
            steps {
                echo "Uploading artifact..."
                // Your artifact upload steps here
                // Use params.BUILD and params.UPLOAD_ARTIFACT to conditionally execute steps
            }
        }

        stage('Run Test Stage Parallel') {
            parallel {
                stage('Test1') {
                    when {
                        expression { params.BUILD }
                    }
                    steps {
                        echo 'Running Test1...'
                        // Your test commands for Test1
                    }
                }

                stage('Test2') {
                    when {
                        expression { params.BUILD }
                    }
                    steps {
                        echo 'Running Test2...'
                        // Your test commands for Test2
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Your deployment steps here
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! Deploying to production...'
            // Add deployment to production steps here
        }
        failure {
            echo 'Pipeline failed! Not deploying to production.'
        }
    }
}
