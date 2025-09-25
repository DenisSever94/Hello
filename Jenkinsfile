pipeline {
    agent {
        docker {
            image 'maven:3.9.3-eclipse-temurin-17' // Maven + JDK17 готовый образ
            args '-v /var/jenkins_home/.ssh:/root/.ssh:ro' // подключаем SSH ключи Jenkins
        }
    }

    stages {
        stage('Checkout') {
            steps {
                sshagent(credentials: ['02131aea-794a-48e7-af64-51a05008ad20']) {
                    git branch: 'main',
                        url: 'git@github.com:DenisSever94/Hello.git'
                }
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
                echo 'Deploy stage skipped'
            }
        }
    }

    post {
        success { echo 'Сборка успешно завершена!' }
        failure { echo 'Сборка провалена!' }
    }
}
