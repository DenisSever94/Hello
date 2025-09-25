pipeline {
    agent any

    environment {
        MVN_HOME = tool name: 'Maven 3.9.1', type: 'maven' // замени на установленный Maven в Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                sshagent(['02131aea-794a-48e7-af64-51a05008ad20']) {
                    sh 'rm -rf Hello || true' // чистим старый workspace
                    sh 'git clone -b main git@github.com:DenisSever94/Hello.git'
                    dir('Hello') {
                        sh 'git status' // проверяем, что мы внутри репо
                    }
                }
            }
        }

        stage('Build') {
            steps {
                dir('Hello') {
                    sh "${MVN_HOME}/bin/mvn clean install"
                }
            }
        }

        stage('Test') {
            steps {
                dir('Hello') {
                    sh "${MVN_HOME}/bin/mvn test"
                }
            }
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
