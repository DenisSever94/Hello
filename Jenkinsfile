pipeline {
    agent any

    tools {
        git 'Default'  // убедись, что Git установлен и указан как Default
        maven 'Maven3'  // или имя твоей Maven установки в Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Запуск ssh-agent для использования credentials
                sshagent(credentials: ['02131aea-794a-48e7-af64-51a05008ad20']) {
                    git branch: 'main',
                        url: 'git@github.com:DenisSever94/Hello.git'
                }
            }
        }

        stage('Build') {
            steps { sh 'mvn clean install' }
        }

        stage('Test') {
            steps { sh 'mvn test' }
        }

        stage('Deploy') {
            steps { echo 'Deploy stage skipped' }
        }
    }

    post {
        success { echo 'Сборка успешно завершена!' }
        failure { echo 'Сборка провалена!' }
    }
}
