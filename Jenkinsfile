pipeline {
    agent none

    tools {
        
        gradle 'Gradle3'
        maven "M3"
        jdk "OpenJDK-17"
    }

    stages {
        stage('Preparation') {
            agent { label 'node1' } 
            steps {
                checkout scm
            }
        }

        stage('Build') {
            
            agent { label 'node1' } 
            steps {
                // Ejecutar Gradle para compilar y ejecutar pruebas unitarias
                sh "mvn test"
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
