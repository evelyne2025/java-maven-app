pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/evelyne2025/java-maven-app.git'
            }
        }

        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('Build Artifact') {
            steps {
                sh "mvn package"
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                   withDockerRegistry(credentialsId: 'docker-cred', url: 'https://hub.docker.com/repositories/eveojong') {
                            sh "docker build -t eveojong/java-maven-app:1.0 ."
                   }    
                }     
            } 
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', url: 'https://hub.docker.com/repositories/eveojong') {
                    sh "docker push eveojong/java-maven-app:1.0"
                    }
                } 
            }
        }
    }
}
