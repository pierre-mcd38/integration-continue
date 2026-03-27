pipeline {
    agent any // Indique que le pipeline peut s'exécuter sur n'importe quel agent disponible

    stages {
        stage('Connexion SCM') {
            steps {
                echo 'Récupération du code depuis GitHub réussie.'
            }
        }
        stage('Validation Livrable') {
            steps {
                echo 'Le pipeline par défaut est opérationnel.'
                sh 'echo "Date de l execution : `date`"'
            }
        }
    }
}