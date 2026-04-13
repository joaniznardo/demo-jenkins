pipeline {
    agent { label 'linux' }

    options {
        timeout(time: 30, unit: 'MINUTES')
        retry(2)
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }

    stages {

        stage('Build') {
            steps {
                echo "🔨 Compilant l'aplicació..."
                //sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Executant proves..."
                //sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Desplegant a producció..."
                //sh './deploy.sh'
            }
        }

    }

    post {
        always {
            echo "🧹 Neteja finalitzada."
            //sh 'rm -rf target/'
        }
        success {
            echo "✅ Desplegament completat amb èxit!"
        }
        failure {
            echo "❌ Alguna cosa ha anat malament. Revisa els logs."
        }
    }
}
