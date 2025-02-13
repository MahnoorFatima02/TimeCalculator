
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:MahnoorFatima02/TimeCalculator.git'
            }
        }

        stage('Build') {
            steps {
                     sh '''
                                export MAVEN_HOME=/opt/homebrew/Cellar/maven/3.9.9/libexec
                                export PATH=$MAVEN_HOME/bin:$PATH
                                echo "Using Maven from: $(which mvn)"
                                mvn clean install
                            '''
            }
        }

        stage('Test') {
            steps {
                   sh '''
                               export MAVEN_HOME=/opt/homebrew/Cellar/maven/3.9.9/libexec
                               export PATH=$MAVEN_HOME/bin:$PATH
                               mvn test
                           '''
            }
        }

        stage('Code Coverage') {
            steps {
                jacoco execPattern: '**/target/jacoco.exec'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            jacoco execPattern: '**/target/jacoco.exec'
        }
    }
}

