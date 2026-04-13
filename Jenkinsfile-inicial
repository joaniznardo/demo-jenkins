pipeline {
    agent { label 'linux' }

    // Definim els paràmetres d'entrada que l'usuari veurà al formulari
    parameters {
        choice(
            name: 'AMBIENT',
            choices: ['DEV', 'QA', 'PROD'],
            description: 'Destí del desplegament'
        )
        booleanParam(
            name: 'MODE_DEBUG',
            defaultValue: false,
            description: 'Activar logs detallats?'
        )
    }

    environment {
        NOM_APP = "LaMevaApp"
        // Executem una comanda shell per obtenir la data actual i la guardem com a variable
        DATA = sh(returnStdout: true, script: 'date +%Y-%m-%d').trim()
    }

    stages {

        stage('Configuració') {
            steps {
                echo "🚀 Desplegant ${env.NOM_APP} amb data ${env.DATA}"
                echo "🌍 Destí seleccionat: ${params.AMBIENT}"
            }
        }

        stage('Lògica Condicional') {
            steps {
                // ⚠️ OJO: El bloc 'if' requereix un bloc 'script' dins del Pipeline Declaratiu
                script {

                    // Comprovem si estem desplegant a Producció
                    if (params.AMBIENT == 'PROD') {
                        echo "⚠️ ATENCIÓ: ESTÀS MODIFICANT PRODUCCIÓ ⚠️"
                        echo "Assegura't que tens aprovació del teu equip abans de continuar."
                    } else {
                        echo "✅ Entorn segur: ${params.AMBIENT} — pots continuar sense risc."
                    }

                    // Si el mode debug està activat, imprimim totes les variables d'entorn
                    if (params.MODE_DEBUG) {
                        echo "🔍 Mode DEBUG activat — mostrant totes les variables d'entorn:"
                        sh 'printenv | sort'  // 'sort' per facilitar la lectura
                    }

                }
            }
        }

    }
}
