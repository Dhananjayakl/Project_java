pipeline {
    agent { label 'Node-2' }

    options {
        timestamps()
    }

    tools {
        maven 'Maven3'
        jdk 'openjdk21'
    }

    environment {
        GIT_REPO = 'https://github.com/Dhananjayakl/Project_java.git'
        BRANCH   = 'main'
    }

    stages {

        stage('Checkout repo') {
            steps {
                git branch: "${BRANCH}",
                    url: "${GIT_REPO}",
                    credentialsId: '246e4390-6513-40d3-9379-a13be88e6658'
            }
        }

        stage('Build') {
            steps {
                echo 'Running maven build...'
                dir('maven') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit Tests') {
            steps {
                dir('maven') {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit allowEmptyResults: true,
                          testResults: '**/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
