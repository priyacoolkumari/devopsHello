pipeline {
    agent any
tools{
maven 'Maven'
}


    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_PROJECT_KEY = 'priyacoolkumari_java-hello-world-with-maven_fbd14a2b-1fee-4680-a5ec-72f43255788e'
        SONAR_TOKEN = credentials('sonar-token')  // Fetches the token securely from Jenkins credentials
    }

    stages {
        stage('Checkout') {

            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/priyacoolkumari/devopsHello.git']]
                ])
            }
        }
                stage('Build Backend and SonarQube Analysis') {
                    steps {
                        echo "Starting Build Backend stage..."
                        sh 'echo "Current directory: $(pwd)"'
                        sh 'echo "Listing files in workspace:" && ls -la'
                        withSonarQubeEnv('Sonar') { // Ensure 'SonarQube' matches the configured SonarQube server in Jenkins
                            sh "mvn clean verify sonar:sonar -Dsonar.projectKey=priyacoolkumari_java-hello-world-with-maven_fbd14a2b-1fee-4680-a5ec-72f43255788e -Dsonar.projectName='java-hello-world-with-maven'"
                        }
                        echo "Build process complete. Checking target directory contents..."
                        sh 'ls -la target'
                    }
                }
    }
}
