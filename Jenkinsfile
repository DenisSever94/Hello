pipeline {
    agent {
        docker {
            image 'maven:3.9.3-eclipse-temurin-17' // Maven + JDK17
            args '-v /root/.m2:/root/.m2 -v /var/jenkins_home/.ssh:/root/.ssh:ro' 
            // монтируем локальный кэш Maven и SSH ключи
        }
    }

    environment {
        GIT_SSH_COMMAND = 'ssh -i /root/.ssh/id_ed25519 -o StrictHostKeyChecking=no'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:DenisSever94/Hello.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // sh './deploy.sh' // если есть скрипт deploy
            }
        }
    }
}
