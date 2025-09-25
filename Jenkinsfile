pipeline {
    agent any

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
