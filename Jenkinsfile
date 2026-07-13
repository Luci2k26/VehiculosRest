pipeline {
    agent any
    stages {
        stage('Compilación') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Crear Imagen Docker') {
            steps {
                // Creacion de Imagen docker
                sh 'docker build -t mi-app-tomcat .'
            }
        }
        stage('Despliegue Tomcat') {
            steps {
                // clean and build de contenedores
                sh 'docker stop servidor-tomcat || true'
                sh 'docker rm servidor-tomcat || true'
                sh 'docker run -d -p 9090:8080 --name servidor-tomcat mi-app-tomcat'
            }
        }
    }
}