pipeline {
    
    agent {label 'docker'}

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Код загружен. Ищем SQL скрипт..."
            }
        }

        stage('Run SQL Query') {
            steps {
                echo "Запуск скрипта: query.sql"
                sh 'mysql -h rfam-db.ebi.ac.uk -P 4497 -u rfamro -D Rfam < ./query.sql'
            }
        }
    }

    post {
        always {
            echo 'Пайплайн завершен.'
        }
        success {
            echo 'SQL-запрос выполнен успешно.'
        }
        failure {
            echo 'ОШИБКА: Пайплайн не удался.'
        }
    }
}
