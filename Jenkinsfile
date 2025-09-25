pipeline {
    agent any

    environment {
        REPO_URL = 'git@github.com:DenisSever94/Hello.git'
        REPO_DIR = 'Hello'
    }

    stages {
        stage('Checkout Git via SSH') {
            steps {
                sshagent(['git']) {  // ID SSH credentials в Jenkins
                    script {
                        if (!fileExists(REPO_DIR)) {
                            sh "git clone ${REPO_URL} ${REPO_DIR}"
                        }
                        dir(REPO_DIR) {
                            sh '''
                                git fetch --all
                                git reset --hard origin/main
                            '''
                        }
                    }
                }
            }
        }

        stage('Build') {
            steps {
                dir(REPO_DIR) {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                dir(REPO_DIR) {
                    sh 'mvn test'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Сборка успешно завершена!'
        }
        failure {
            echo '❌ Сборка провалилась!'
        }
    }
}
