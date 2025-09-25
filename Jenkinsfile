pipeline {
    agent any

    environment {
        MVN_HOME = tool name: 'Maven 3.9.1', type: 'maven' // замени на свой Maven
    }

    stages {
        stage('Checkout') {
            steps {
                sshagent(['02131aea-794a-48e7-af64-51a05008ad20']) {
                    // очищаем предыдущий workspace, если есть
                    sh 'rm -rf Hello || true'
                    // клонируем репо прямо через SSH
                    sh 'git clone -b main git@github.com:DenisSever94/Hello.git'
                }
            }
        }

        stage('Build & Test') {
            steps {
                dir('Hello') {
                    sh "${MVN_HOME}/bin/mvn clean install test"
                }
            }
        }
    }

    post {
        success { echo 'Сборка успешно завершена!' }
        failure { echo 'Сборка провалена!' }
    }
}
