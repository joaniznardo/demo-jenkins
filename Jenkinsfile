pipeline {
    agent { label 'linux' } // Forcem l'execució a l'Agent del Dia 1

    stages {

        stage('Reconeixement') {
            steps {
                echo 'Hola, estic iniciant...'
                sh 'hostname'  // Mostra el nom de la màquina on s'executa
                sh 'whoami'    // Mostra l'usuari amb què s'executa Jenkins
            }
        }

        stage('Variables d\'Entorn') {
            steps {
                // Imprimim totes les variables que Jenkins injecta per defecte
                sh 'printenv'
            }
        }

    }
}
