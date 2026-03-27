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
                sh './venv/bin/python -m py_compile app.py'
            }
        }

        stage('4. Tests Unitaires & E2E') {
            steps {
                sh './venv/bin/pytest test_app.py'
            }
        }

        stage('5. Archivage de la Release') {
            steps {
                echo 'Création du paquet déployable...'
                // On crée une archive contenant le code et les dépendances
                sh 'tar -czvf release-app.tar.gz app.py requirements.txt'
                
                // Cette commande Jenkins archive officiellement le fichier dans l'interface
                archiveArtifacts artifacts: 'release-app.tar.gz', fingerprint: true
            }
        }

        stage('6. Test de fumée (Smoke Test)') {
            steps {
                echo 'Vérification de l intégrité de l artefact...'
                // On vérifie simplement si l'archive créée n'est pas vide
                sh 'test -s release-app.tar.gz'
                echo 'L artefact est prêt pour le déploiement.'
            }
        }
    }

    post {
        success {
            echo 'Félicitations : Pipeline de CI/CD complet terminé avec succès !'
        }
    }
}