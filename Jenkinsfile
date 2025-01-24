pipeline {
    agent any

    environment {
      dockerImage = ''
      registry = 'bridgetching9528/abcapp'
      registryCredential = 'Dockerhub-login'
    }

    tools {
        maven 'maven' // Replace with your Maven installation name in Jenkins
        jdk 'JDK 17'      // Replace with the required JDK version
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
        stage('Build Docker Image') {
            steps {
                script {
                    // Replace 'your-image-name' with the desired Docker image name
                    sh 'docker build -t bridgetching9528/abcapp .'
                }
            }
        }
    }
        stage('Push image to Hub') {
            steps {
                script {
                    // make sure you install the docker pipeline pluging
                    docker.withRegistry('', registryCredential) {
                    sh 'docker push bridgetching9528/abcapp'
                }
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        }
        failure {
            echo 'Build failed!'
        }
    }
}
