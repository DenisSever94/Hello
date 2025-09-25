pipeline {
    agent any

    tools {
        maven 'Maven 3.9.3' // если Maven установлен через Manage Jenkins -> Global Tool Configuration
        jdk 'JDK17'          // если JDK установлен
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
                // sh './deploy.sh' // если есть deploy скрипт
            }
        }
    }
}
