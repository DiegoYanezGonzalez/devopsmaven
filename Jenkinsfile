pipeline {
    agent any

    tools {
        maven 'Maven3'       // Nombre configurado en Jenkins → Global Tools
        jdk 'JDK17'          // Nombre configurado en Jenkins → Global Tools
    }


    stages {
      stage('Checkout') {
    steps {
        checkout([$class: 'GitSCM',
            branches: [[name: '*/main']],  // <- cambia aquí
            userRemoteConfigs: [[url: 'https://github.com/DiegoYanezGonzalez/devopsmaven']]
        ])
    }
}


        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completado con éxito.'
        }
        failure {
            echo 'El build falló.'
        }
    }
}
