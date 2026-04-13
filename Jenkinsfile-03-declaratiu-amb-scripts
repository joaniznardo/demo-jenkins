pipeline {
    agent { label 'linux' }

    stages {

        stage('Comprovació del Sistema') {
            steps {
                script {
                    echo "🔍 Detectant la versió de Java instal·lada al sistema..."

                    // 1. Executem la comanda shell
                    // 2. returnStdout: true  → Captura la sortida com a text
                    // 3. .trim()             → Elimina espais i salts de línia finals
                    def versioJava = sh(
                        script: 'java -version 2>&1 | head -n 1 | awk -F \'"\' \'{print $2}\'',
                        returnStdout: true
                    ).trim()

                    echo "📦 Versió detectada: ${versioJava}"

                    // Guardem el resultat en una variable global d'entorn
                    // perquè sigui accessible des d'altres stages
                    env.JAVA_DETECTADA = versioJava
                }
            }
        }

        stage('Validació') {
            steps {
                script {
                    echo "🧪 Validant que la versió de Java és la requerida..."

                    // Usem el mètode .startsWith() de String (Groovy/Java)
                    // per comprovar que la versió comença per "21"
                    if (env.JAVA_DETECTADA.startsWith("21")) {
                        echo "✅ Versió correcta: Java ${env.JAVA_DETECTADA}"
                        echo "El sistema compleix els requisits mínims. Continuem."
                    } else {
                        // error() força el fail del Pipeline amb un missatge clar
                        error "❌ Versió incorrecta. Es requereix Java 21. Trobat: ${env.JAVA_DETECTADA}"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                // Aquest stage només s'executa si la validació ha passat
                echo "🔨 Prerequisits validats. Iniciant compilació..."
                //                sh 'mvn --version'  // Comprovem que Maven també és accessible
            }
        }

    }

    post {
        success {
            echo "✅ Pipeline completat. Java ${env.JAVA_DETECTADA} validat correctament."
        }
        failure {
            echo "❌ Pipeline aturat. Revisa la versió de Java del sistema."
            echo "Versió trobada: ${env.JAVA_DETECTADA ?: 'No s\\'ha pogut detectar'}"
        }
    }
}
