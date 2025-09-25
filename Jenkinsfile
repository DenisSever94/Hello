pipeline {
    agent any

 tools {
    git 'Default'
}

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:DenisSever94/Hello.git',
                    credentialsId: '02131aea-794a-48e7-af64-51a05008ad20'
            }
        }

        stage('Build') {
            steps { sh 'mvn clean install' }
        }

        stage('Test') {
            steps { sh 'mvn test' }
        }

        stage('Deploy') {
            steps { /* sh './deploy.sh' */ }
        }
    }

    post {
        success { echo 'Сборка успешно завершена!' }
        failure { echo 'Сборка провалена!' }
    }
}
