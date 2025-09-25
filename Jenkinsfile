pipeline {
    agent any

    stages {
        stage('Checkout Git via SSH') {
            steps {
                sshagent(['git']) {  // ID credentials из Jenkins
                    sh '''
                        if [ ! -d "Hello" ]; then
                            git clone git@github.com:DenisSever94/Hello.git
                        fi
                        cd Hello
                        git fetch --all
                        git reset --hard origin/main
                    '''
                }
            }
        }

        stage('Build') {
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
