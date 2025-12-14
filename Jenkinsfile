pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ale28ab/ProyectoAleMilton.git'
            }
        }

        stage('Build') {
            steps {
                echo "Compilando el proyecto..."
            }
        }

        stage('Test') {
            steps {
                echo "Ejecutando pruebas..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Desplegando proyecto..."
            }
        }
    }

    post {
        always {
            echo "Pipeline finalizado."
        }
    }
}