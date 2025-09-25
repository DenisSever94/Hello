pipeline {
    agent any

    environment {
        // Указываем путь к Maven, если не настроен глобально
        MAVEN_HOME = tool name: 'Maven', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Git') {
            steps {
                // Используем SSH ключ, который уже работает
                sshagent(['git']) { // <-- ID credentials из Jenkins
                    // Клонируем репозиторий, если папки нет, иначе обновляем
                    sh '''
                        if [ ! -d "Hello" ]; then
                            git clone git@github.com:DenisSever94/Hello.git
                        fi
                        cd Hello
                        git pull
                    '''
                }
            }
        }

        stage('Build with Maven') {
            steps {
                sh '''
                    cd Hello
                    mvn clean install
                '''
            }
        }
    }

    post {
        success {
            echo 'Сборка успешно завершена!'
        }
        failure {
            echo 'Сборка провалилась!'
        }
    }
}
