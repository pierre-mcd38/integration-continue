pipeline {
    agent any

    stages {
        stage('1. Récupération des sources') {
            steps {
                checkout scm
            }
        }

        stage('2. Mise à jour des dépendances') {
            steps {
                sh '''
                    python3 -m venv venv
                    ./venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('3. Compilation / Linting') {
            steps {
                // On utilise le python de l'environnement virtuel
                sh './venv/bin/python -m py_compile app.py'
            }
        }

        stage('4. Tests Unitaires & E2E') {
            steps {
                // On utilise le pytest installé dans l'environnement virtuel
                sh './venv/bin/pytest test_app.py'
            }
        }
    }
}