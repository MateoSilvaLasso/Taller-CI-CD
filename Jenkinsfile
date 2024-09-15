pipeline {
    agent none // No usar ningún agente por defecto

    tools {
        // Instalar la versión de Gradle configurada como "Gradle3" y agregarla al path.
        gradle 'Gradle3'
    }

    stages {
        stage('Preparation') {
            agent { label 'node1' } 
            steps {
                // Obtener el código del repositorio actual (donde se encuentra este script)
                checkout scm
            }
        }

        stage('Build') {
            
            agent { label 'node1' } // Nodo 1 para build y pruebas unitarias
            steps {
                // Ejecutar Gradle para compilar y ejecutar pruebas unitarias
                sh "./gradlew clean build"
            }
            post {
                // Almacenar los resultados de las pruebas unitarias
                success {
                    junit '**/build/test-results/test/*.xml'
                    archiveArtifacts 'build/libs/*.jar'
                }
            }
            
        }

        
    }
}
