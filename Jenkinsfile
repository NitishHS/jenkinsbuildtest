pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven 3', type: 'hudson.tasks.Maven$MavenInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your version control system
                git 'https://your-repository-url.git'
            }
        }
        
        stage('Build') {
            steps {
                // Run the Maven build
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }
        
        stage('Test') {
            steps {
                // Run the Maven tests
                sh "${MAVEN_HOME}/bin/mvn test"
            }
            post {
                always {
                    // Archive test results
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application
                sh "${MAVEN_HOME}/bin/mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                }
            }
        }
    }
    
    post {
        always {
            // Clean up the workspace
            cleanWs()
        }
    }
}