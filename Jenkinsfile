
pipeline {
    agent any

    environment {
        JAVA_HOME = '/opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk/Contents/Home'
        PATH = "/opt/homebrew/opt/openjdk@21/bin:/opt/homebrew/bin:${env.PATH}"
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
                echo 'Checking Java version...'
                sh '"$JAVA_HOME/bin/java" -version'

                echo 'Checking Maven installation...'
                sh 'which mvn'
                sh 'mvn -version'
            }
        }

        stage('Clean and Build') {
            steps {
                echo 'Building the project with Maven...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Maven tests...'
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving generated JAR files...'
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
            echo 'Maven build and tests completed successfully.'
            echo 'Artifacts archived successfully.'
        }

        failure {
            echo 'BUILD FAILED! Check the Console Output for details.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}