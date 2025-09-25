pipeline {
    agent {
        docker {
            image 'maven:3.9.3-eclipse-temurin-17' // Maven + JDK17
            args '-v /root/.m2:/root/.m2' // кэш локального репозитория Maven (опционально)
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
                // Если у тебя нет скрипта deploy.sh, убери или закомментируй эту строку
                // sh './deploy.sh'
            }
        }
    }
}
