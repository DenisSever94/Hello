pipeline {
    agent any

    environment {
        SSH_CREDENTIALS = '02131aea-794a-48e7-af64-51a05008ad20' // твой глобальный SSH ключ
        IMAGE_NAME = 'hello-app'
        IMAGE_TAG = 'latest'
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

        stage('Build Docker Image') {
            steps {
                dir('Hello') {
                    sh """
                        docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                    """
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                        docker push ${DOCKER_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Сборка, тесты и деплой Docker прошли успешно!'
        }
        failure {
            echo '❌ Что-то пошло не так на этапе сборки/теста/деплоя!'
        }
    }
}
