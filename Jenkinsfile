pipeline {
    agent any

    stages {
        stage('Git clone'){
            steps {
                echo 'Clonage du repo'
                checkout scm
                sh 'ls -la'
            }
        }
        stage('Build'){
            steps{
                echo 'Compilation du projet'
                sh 'mvn compile'
            }
        }
        stage('Test'){
            steps{
                dir('src') {
                    echo 'Test unitaire'
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts 'src/target/surefire-reports/*.xml'
        }
        success {
            echo 'Cest un succes'
        }
        failure {
            echo 'Cest un echec'
        }
    }

}