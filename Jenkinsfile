pipeline {
    agent any

    stages {
        stage('Checkout Repo') {
            steps {
                sshagent(['02131aea-794a-48e7-af64-51a05008ad20']) {
                    // Клонируем репо прямо в workspace
                    sh '''
                        rm -rf Hello || true
                        git clone git@github.com:DenisSever94/Hello.git
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                dir('Hello') {
                    // Если у тебя Maven, можно заменить на Gradle или другой билд
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                dir('Hello') {
                    sh 'mvn test'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Сборка прошла успешно!'
        }
        failure {
            echo '❌ Сборка провалилась!'
        }
    }
}
