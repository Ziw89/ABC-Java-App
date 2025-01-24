# ABC-Java-App
Java App for CI/CD learning projects

## Building App with CLI Commands:
```
mvn compiler:compile
mvn test
mvn package
```

## Using Jenkinsfile to automate this build:
```
pipeline {
    agent any

    tools {
        maven 'Maven 3.x' // Replace with your Maven installation name in Jenkins
        jdk 'JDK 11'      // Replace with the required JDK version
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from your repository
                checkout scm
            }
        }
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compiler:compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        failure {
            echo 'Build failed!'
        }
    }
}
```
