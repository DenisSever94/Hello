pipeline {
    agent any

    tools {
        git 'Default'
        jdk 'JDK17'
        maven 'Maven3' // или имя Maven, как в твоей конфигурации
    }

    stages {
        stage('Checkout') {
            steps {
                sshagent(['02131aea-794a-48e7-af64-51a05008ad20']) {
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
