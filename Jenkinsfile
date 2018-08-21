pipeline {
    agent any

    maven 'Maven 3.5.4'
    jdk   'Java'
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
            post {
              success {
                junit 'target/surefire-reports/**/*.xml'
              }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn -Dmaven.test.failure.ignore=true test'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging....'
                sh 'mvn -DskipTest package'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
