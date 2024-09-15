pipeline {
    agent any
    
    tools {
        jdk 'jdk11'  // Make sure to have JDK 11 configured in Jenkins
        gradle 'gradle-7.4'  // Make sure to have Gradle 7.4 configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh './gradlew build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'
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
