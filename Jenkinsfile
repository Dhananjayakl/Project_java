pipeline {
    agent { label 'NODE-1' }

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
                    credentialsId: 'ssh-wsl'
            }
        }

        stage('Build') {
            steps {
                echo 'Running maven build...'
                    sh 'mvn clean package'
            }
        }

        stage('Unit Tests') {
            steps {
                    sh 'mvn test'
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
