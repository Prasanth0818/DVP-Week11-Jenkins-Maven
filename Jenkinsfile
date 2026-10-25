
pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/opt/homebrew/opt/maven/bin:${env.PATH}"
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Java and Maven') {
            steps {
                sh 'echo "Checking Java..."'
                sh 'java -version'
                sh 'echo "Checking Maven..."'
                sh 'which mvn'
                sh 'mvn -version'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts(
                    artifacts: 'target/*.jar',
                    fingerprint: true
                )
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESSFUL!'
            echo 'Maven build completed and artifacts archived.'
        }

        failure {
            echo 'BUILD FAILED! Check the console output.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}