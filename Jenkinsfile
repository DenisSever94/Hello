pipeline {
    agent any

    environment {
        SSH_CREDENTIALS = '02131aea-794a-48e7-af64-51a05008ad20' // твой глобальный ключ
    }

    stages {
        stage('Checkout Repo') {
            steps {
                sshagent([env.SSH_CREDENTIALS]) {
                    sh '''
                        echo "Клонируем репозиторий через SSH"
                        rm -rf Hello || true
                        git clone git@github.com:DenisSever94/Hello.git
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                dir('Hello') {
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
