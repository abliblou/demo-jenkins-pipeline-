pipeline {
    agent {
        docker { image 'maven:sapmachine'}
    }

    stages {
        stage('Git clone'){
            steps {
                dir('src') {
                    echo 'Clonage du repo'
                    checkout scm
                    sh 'ls -la'
                }
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
            archiveArtifacts 'target/surefire-reports/*.xml'
        }
        success {
            echo 'Cest un succes'
        }
        failure {
            echo 'Cest un echec'
        }
    }

}