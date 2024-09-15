pipeline {
    agent any
    tools {
        gradle 'gradle'  // Make sure to have Gradle 7.4 configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        stage('Tool Check') {
            steps {
                withGradle {
                    sh 'gradle --version'
                }
            }
        }
        stage('Build') {
            steps {
                withGradle {
                    echo 'Building the project...'
                    sh 'gradlew build'
                }
            }
        }
        stage('Test') {
            steps {
                withGradle {
                    echo 'Running tests...'
                    sh 'gradlew test'
                }
            }
        }
        stage('Publish Test Results') {
            steps {
                echo 'Publishing test results...'
                junit '**/build/test-results/test/*.xml'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
            // Archive build artifacts if needed
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
    }
}
