pipeline {
    agent any

    stages {
        stage('1. Récupération des sources') {
            steps {
                checkout scm
                echo 'Code source récupéré.'
            }
        }

        stage('2. Mise à jour des dépendances') {
            steps {
                // On installe les bibliothèques listées dans requirements.txt
                sh 'pip install -r requirements.txt'
            }
        }

        stage('3. Compilation / Linting') {
            steps {
                echo 'Vérification de la syntaxe Python...'
                // 'python -m py_compile' vérifie s'il y a des erreurs de syntaxe
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('4. Tests Unitaires & E2E') {
            steps {
                echo 'Exécution des tests avec Pytest...'
                sh 'pytest test_app.py'
            }
        }
    }
}