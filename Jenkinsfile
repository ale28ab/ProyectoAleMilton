pipeline {
    agent any

    stages {
<<<<<<< HEAD
=======

>>>>>>> eaab140 (Estructura inicial del proyecto con Docker y Jenkins)
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ale28ab/ProyectoAleMilton.git'
            }
        }

<<<<<<< HEAD
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
=======
        stage('Docker Build (Compose)') {
            steps {
                echo 'Construyendo imagen Docker'
                sh 'docker compose build'
            }
        }

        stage('Docker Run (Validación)') {
            steps {
                echo 'Ejecutando validación automática'
                sh 'docker compose up --abort-on-container-exit'
>>>>>>> eaab140 (Estructura inicial del proyecto con Docker y Jenkins)
            }
        }
    }

    post {
        always {
<<<<<<< HEAD
            echo "Pipeline finalizado."
        }
    }
}
=======
            echo 'Pipeline finalizado'
        }
    }
}
>>>>>>> eaab140 (Estructura inicial del proyecto con Docker y Jenkins)
