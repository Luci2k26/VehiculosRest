pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Obtener Código') {
            steps {
                git branch: 'main', credentialsId: 'github-crd', url: 'https://github.com/Luci2k26/VehiculosRest.git'
            }
        }
        stage('Compilación') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Crear Imagen Docker') {
            steps {
                /* Creacion de imagen usando Dockerfile*/
                sh 'docker build -t mi-app-tomcat .'
            }
        }
        stage('Despliegue Tomcat') {
             steps {
                 script {
                     // Verificación de contenedor
                     def containerExists = sh(script: "docker ps -a -q -f name=servidor-tomcat", returnStdout: true).trim()

                     if (containerExists) {
                         sh 'docker stop servidor-tomcat'
                         sh 'docker rm servidor-tomcat'
                     }
                 }
                 // Contenedor nuevo
                 sh 'docker run -d -p 9090:8080 --name servidor-tomcat mi-app-tomcat'
             }
         }
        /*stage('Despliegue Tomcat') {
            steps {
                // Detiene, borra y crea un nuevo contenedor
                sh 'docker stop servidor-tomcat || true'
                sh 'docker rm servidor-tomcat || true'
                sh 'docker run -d -p 9090:8080 --name servidor-tomcat mi-app-tomcat'
            }*/
        }
    }
}