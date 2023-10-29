def artifacturl="https://anshika1.jfrog.io/artifactory/libs-snapshot/Project-1.0.1"
def artifactapitoken="AKCp8pRa4f1D5jB952CH7vSPCNWGPYThdfieG6YxMdogBdTuXxMAPDXgvrtwrw5wP5YwUuvXz"
def artifactausername="X-Jfrog-Art-Api"
def artifactname="my-app-1.0-SNAPSHOT.jar"

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

                if ( ${env.BRANCH_NAME}.startswith("feature") ) {
                // Build your application (replace this with your build commands)
               // def workspaceDir = env.WORKSPACE
                echo "${env.WORKSPACE}"
                //bat 'cd ${env.WORKSPACE}/target'
               // bat 'curl -H "X-Jfrog-Art-Api:AKCp8pRa4f1D5jB952CH7vSPCNWGPYThdfieG6YxMdogBdTuXxMAPDXgvrtwrw5wP5YwUuvXz" -O -L "https://anshika1.jfrog.io/artifactory/libs-snapshot/Project-1.0.1/my-app-1.0-SNAPSHOT.jar" -T "my-app-1.0-SNAPSHOT.jar"'
                bat """
                cd ${env.WORKSPACE}/target
                echo "${env.BRANCH_NAME}"
                echo "${artifacturl}"
                curl -H "${artifactausername}:${artifactapitoken}" -O -L "${artifacturl}/${artifactname}" -T "${artifactname}"
                """    
                }
                else {
                    echo "Not a fearure branch"
                }       
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
