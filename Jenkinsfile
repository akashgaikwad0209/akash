def artifacturl="https://anshika1.jfrog.io/artifactory/libs-snapshot/Project-1.0.1"
def artifactapitoken="AKCp8pRa4f1D5jB952CH7vSPCNWGPYThdfieG6YxMdogBdTuXxMAPDXgvrtwrw5wP5YwUuvXz"
def artifactausername="X-Jfrog-Art-Api"
def artifactname="my-app-1.0-SNAPSHOT.jar"

pipeline {
    agent any  // This runs the pipeline on any available agent (node/agent)

    stages {
        stage('Build') {
            steps {
                // Build your application (replace this with your build commands)
                bat 'mvn clean install'
            }
        }

        stage('Artifact Upload') {
            steps {
                // Build your application (replace this with your build commands)
               // def workspaceDir = env.WORKSPACE
                echo "${env.WORKSPACE}"
                //bat 'cd ${env.WORKSPACE}/target'
               // bat 'curl -H "X-Jfrog-Art-Api:AKCp8pRa4f1D5jB952CH7vSPCNWGPYThdfieG6YxMdogBdTuXxMAPDXgvrtwrw5wP5YwUuvXz" -O -L "https://anshika1.jfrog.io/artifactory/libs-snapshot/Project-1.0.1/my-app-1.0-SNAPSHOT.jar" -T "my-app-1.0-SNAPSHOT.jar"'
                bat """
                cd ${env.WORKSPACE}/target
                echo "${artifacturl}"
                curl -H "${artifactausername}:${artifactapitoken}" -O -L "${artifacturl}/${artifactname}" -T "${artifactname}"
                """           
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
