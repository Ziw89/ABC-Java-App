pipeline {
    agent any

    environment {
      dockerImage = ''
      registry = 'bridgetching9528/abcapp'
      registryCredential = 'Dockerhub-login'
    }

    tools {
        maven 'maven' // Replace with your Maven installation name in Jenkins
    }

        stage('Clone Repository') {
            steps {
                // Clone public repository without credentials
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], // Replace 'main' with your branch
                    userRemoteConfigs: [[
                        url: 'https://github.com/Ngwaabanjong/ABC-Java-App.git' // Replace with your public repository URL
                    ]]
                ])
            }
        }
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
